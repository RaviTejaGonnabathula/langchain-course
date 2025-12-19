# LangChain Basics: Text Summarizer



This repository contains a simple, professional **Hello World** example demonstrating how to build a **Text Summarizer** using **LangChain** and **OpenAI**.

The application takes raw text (a biography of Elon Musk) and generates:
- A concise summary
- Two interesting facts

using OpenAI’s `gpt-4o` model.

---

## Overview

This project is designed for beginners who want to understand:
- How LangChain prompt templates work
- How to connect LangChain with OpenAI models
- How to build and execute a basic LangChain pipeline using LCEL

---

## Prerequisites

Before running this project, ensure you have:

- Python 3.10 or later
- An OpenAI API key

You can create an API key at:
https://platform.openai.com

---

## Installation and Setup

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/langchain-course.git
cd langchain-course
```

---

### Step 2: Install Dependencies

This project requires the following Python packages:

* langchain
* langchain-openai
* python-dotenv

Install using pip:

```bash
pip install langchain langchain-openai python-dotenv
```

Or using uv:

```bash
uv add langchain langchain-openai python-dotenv
```

---

### Step 3: Configure the OpenAI API Key

Create a `.env` file in the root directory of the project.

```env
OPENAI_API_KEY="sk-proj-xxxxxxxxxxxxxxxx"
```

Do not commit this file to version control.

---

## Running the Application

Execute the main script:

```bash
python main.py
```

---

## Sample Output

```text
1. Summary: Elon Musk is a prominent businessman and entrepreneur...
2. Interesting Facts:
   - Musk has Canadian citizenship through his mother.
   - He was the largest donor in the 2024 U.S. presidential election.
```

---

## Code Explanation

Below is a high-level explanation of the key components used in `main.py`.

---

### Prompt Template

The `PromptTemplate` defines the instructions sent to the language model.
It allows dynamic injection of input text using variables.

```python
summary_template = """
given the information {information} about a person I want you to create:
1. A short summary
2. Two interesting facts about them
"""

summary_prompt_template = PromptTemplate(
    input_variables=["information"],
    template=summary_template
)
```

The `{information}` placeholder is replaced at runtime with the biography text.

---

### Language Model

The OpenAI chat model is initialized as follows:

```python
llm = ChatOpenAI(
    temperature=0,
    model="gpt-4o"
)
```

* A temperature of 0 ensures consistent and deterministic output.
* The `gpt-4o` model is used for high-quality text generation.

---

### Chain Construction

LangChain uses the LangChain Expression Language (LCEL) to connect components.

```python
chain = summary_prompt_template | llm
```

This creates a simple pipeline where the prompt is passed directly to the model.

---

### Chain Invocation

The chain is executed by providing input values for the prompt variables.

```python
response = chain.invoke(
    input={"information": information}
)

print(response.content)
```

The model’s generated summary and facts are returned in `response.content`.

---

