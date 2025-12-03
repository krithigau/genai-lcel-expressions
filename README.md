## Design and Implementation of LangChain Expression Language (LCEL) Expressions

### AIM:
To design and implement a LangChain Expression Language (LCEL) expression that utilizes at least two prompt parameters and three key components (prompt, model, and output parser), and to evaluate its functionality by analyzing relevant examples of its application in real-world scenarios.

### PROBLEM STATEMENT:
Develop an LCEL system capable of generating summaries and extracting key points from input data, using prompt templates, language models, and output parsers for structured output.


### DESIGN STEPS:

#### STEP 1:
Create a prompt template with placeholders for a topic and context.

#### STEP 2:
Configure a language model with specified parameters for processing the template.

#### STEP 3:
Define response schemas for structuring the output into a summary and key points.

#### STEP 4:
Implement a function to generate, process, and parse the response using the template, model, and output parser.

#### STEP 5:
Demonstrate functionality using a practical example.

### PROGRAM:
```py
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI
from langchain.output_parsers import StructuredOutputParser, ResponseSchema

template = PromptTemplate(
    input_variables=["subject", "details"],
    template="Provide a summary for {subject} using this context: {details}"
)

model = OpenAI(model="text-davinci-003", temperature=0.7)

schemas = [
    ResponseSchema(name="summary", description="A brief overview of the subject"),
    ResponseSchema(name="highlights", description="Key points of the summary")
]

parser = StructuredOutputParser.from_response_schemas(schemas)

def process_expression(subject, details):
    generated_prompt = template.format(subject=subject, details=details)
    model_response = model(generated_prompt)
    structured_response = parser.parse(model_response)
    return structured_response

topic_input = "Climate Change"
context_input = (
    "Climate change refers to long-term shifts in temperatures and weather patterns, mainly caused by human activities such as burning fossil fuels, deforestation, and industrial processes. "
    "It has led to global warming, rising sea levels, and increased frequency of extreme weather events."
)

output_result = process_expression(topic_input, context_input)

def display_result(data):
    print("Generated LCEL Expression Output:")
    print("\nSummary:")
    print(data.get("summary", "Summary not provided."))
    print("\nHighlights:")
    print(data.get("highlights", "Highlights not provided."))

display_result(output_result)

```

### OUTPUT:
![image](https://github.com/user-attachments/assets/f7a0c472-e642-4ce8-9669-10c24fb0671a)


### RESULT:
The system successfully processes the input parameters, generates a summary, and extracts key points from the context provided. This demonstrates the functionality of LangChain Expression Language (LCEL) expressions, utilizing a prompt, language model, and output parser to produce structured responses.
