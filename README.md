# 🕵️‍♂️ Building AI Agents that Use Code

This notebook demonstrates how to build **code-capable AI agents** that interact with external tools, using the [`smolagents`](https://github.com/huggingface/smolagents) library and Hugging Face Inference APIs.

Think of it like giving Alfred (from Batman) his own smart assistant that can search, compute, and execute code-based actions to get tasks done. 💪

## 🚀 Features Covered

* Installing and using `smolagents`
* Authenticating with Hugging Face Inference API
* Defining custom tools using the `@tool` decorator
* Pushing tools to huggingface space
* Calling tools from huggingface
* Running a **`CodeAgent`** that executes tasks by calling these tools
* Example: Finding the best-rated catering services in Gotham City using a custom search tool.

## 📦 Dependencies

Make sure you have the following installed:

```bash
pip install smolagents
pip install huggingface_hub
```

You'll also need to log in to your Hugging Face account for API access:

```python
from huggingface_hub import notebook_login
notebook_login()
```

## 🛠 Example Tool

Here's a snippet of a custom tool defined in the notebook:

```python
from smolagents import tool

@tool
def catering_service_tool(query: str) -> str:
    services = {
        "Gotham Catering Co.": 4.9,
        "Wayne Manor Catering": 4.8,
        "Gotham City Events": 4.7,
    }
    best_service = max(services, key=services.get)
    return best_service
```

## 🤖 Running an Agent

```python
from smolagents import CodeAgent, HfApiModel

agent = CodeAgent(
    tools=[catering_service_tool],
    model=HfApiModel()
)

result = agent.run("Can you give me the name of the highest-rated catering service in Gotham City?")
print(result)
```
