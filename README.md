## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:
```
To develop a Python-based application using LangChain Expression Language (LCEL) that dynamically generates structured, audience-specific explanations of complex technical and business domains (such as Artificial Intelligence, Customer Service Chatbots, and Machine Learning in Healthcare) by seamlessly integrating prompt templates, language models, and output parsers into a unified pipeline.
```
### DESIGN STEPS:
```
Load environment variables and set up the OpenAI API key securely.

Define a ChatPromptTemplate taking {topic} and {audience} parameters to structure the output.

Instantiate the ChatOpenAI language model and a StrOutputParser for string response parsing.

Construct an LCEL pipeline by chaining the components together: chain = prompt | model | output_parser.

Invoke the chain with different topic-audience pairs and display the formatted output.
```

### PROGRAM:
```
import os
from dotenv import load_dotenv

from langchain_core.prompts import ChatPromptTemplate
from langchain_openai import ChatOpenAI
from langchain_core.output_parsers import StrOutputParser

# Load API key
load_dotenv()

# Component 1: Prompt Template
prompt = ChatPromptTemplate.from_template(
    """
    Explain {topic} for {audience}.

    Give:
    1. A simple definition
    2. Three important points
    3. One real-world example
    """
)

# Component 2: Language Model
model = ChatOpenAI(
    model="gpt-4o-mini",
    temperature=0.7,
    api_key=os.getenv("OPENAI_API_KEY")
)

# Component 3: Output Parser
output_parser = StrOutputParser()

# LCEL Expression
chain = prompt | model | output_parser

# Example 1: Education
print("EXAMPLE 1 - EDUCATION")

result1 = chain.invoke({
    "topic": "Artificial Intelligence",
    "audience": "Engineering Students"
})

print(result1)


# Example 2: Business
print("\nEXAMPLE 2 - BUSINESS")

result2 = chain.invoke({
    "topic": "Customer Service Chatbots",
    "audience": "Business Owners"
})

print(result2)


# Example 3: Healthcare
print("\nEXAMPLE 3 - HEALTHCARE")

result3 = chain.invoke({
    "topic": "Machine Learning in Healthcare",
    "audience": "Healthcare Students"
})

print(result3)
```
### OUTPUT:
<img width="1007" height="788" alt="Screenshot 2026-11-02 155337" src="https://github.com/user-attachments/assets/8acf7ce6-ef58-4a52-8039-d9b5d925930a" />

### RESULT:
The LCEL chain was successfully built using prompt template, model, and output parser components to dynamically process two input parameters. The application executed across three real-world domains (education, business, and healthcare), producing well-structured, target-audience-tailored outputs.
