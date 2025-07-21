# Personal Email Assistant with LangGraph


A smart email assistant powered by LLMs and LangGraph to automatically triage emails, draft replies, and manage your Gmail inbox with human-in-the-loop control.

## About The Project

This project is a smart email assistant designed to connect directly to a Gmail account. It uses the power of Large Language Models (LLMs) and LangGraph to automate email management. The assistant improves its performance over time by learning from your interactions and feedback.

### Key Features

* **Connect to Gmail**: Securely access your inbox using the Gmail API to read new emails.
* **Triage and Prioritize**: Analyze incoming emails to understand their content, classify intent, and determine priority.
* **Draft Responses**: Automatically generate context-aware replies tailored to the email's content.
* **Human-in-the-Loop**: Before any action is taken (like sending a reply or deleting an email), the system waits for your explicit approval, giving you full control over your inbox.
* **Learn from Feedback**: Uses persistent memory to learn from your decisions (e.g., approving, editing, or rejecting drafts), continuously improving its suggestions over time.

## Environment Setup 

### API Keys

* If you don't have an OpenAI API key, you can sign up [here](https://openai.com/index/openai-api/).
* Sign up for LangSmith [here](https://smith.langchain.com/).
* Generate a LangSmith API key.

### Set Environment Variables

* Create a `.env` file in the root directory:
```shell
# Copy the .env.example file to .env
cp .env.example .env
```

* Edit the `.env` file with the following:
```shell
LANGSMITH_API_KEY=your_langsmith_api_key
LANGSMITH_TRACING=true
LANGSMITH_PROJECT="email-assistant"
OPENAI_API_KEY=your_openai_api_key
```


### Package Installation

**Using pip**

```shell
$ python3 -m venv .venv
$ .venv/Scripts/activate
# Ensure you have a recent version of pip (required for editable installs with pyproject.toml)
$ python3 -m pip install --upgrade pip
# Install the package in editable mode
$ pip install -e .
```


## Connecting to APIs  

### Gmail Integration and Deployment

Set up Google API credentials following the instructions in [Gmail Tools README](src/email_assistant/tools/gmail/README.md).

The README also explains how to deploy the graph to LangGraph Platform.

The full implementation of the Gmail integration is in [src/email_assistant/email_assistant_hitl_memory_gmail.py](/src/email_assistant/email_assistant_hitl_memory_gmail.py).




