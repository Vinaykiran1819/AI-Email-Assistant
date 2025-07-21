# Agents in this Repository

## Overview

This repository demonstrates building agents using LangGraph, focusing on an email assistant that can:
- Triage incoming emails
- Draft appropriate responses
- Execute actions (calendar scheduling, etc.)
- Incorporate human feedback
- Learn from past interactions


## Environment Setup

**Using pip**

```bash
# Create and activate a virtual environment
python3 -m venv .venv
.venv/Scripts/activate

# Ensure you have a recent version of pip (required for editable installs with pyproject.toml)
python3 -m pip install --upgrade pip

# Install the package in editable mode
pip install -e .
```

## Agent Implementations

### Scripts 

The repository contains several implementations with increasing complexity in `src/email_assistant`:


1. **Basic Email Assistant** (`email_assistant.py`)
   - Core email triage and response functionality

2. **Human-in-the-Loop** (`email_assistant_hitl.py`) 
   - Adds ability for humans to review and approve actions

3. **Memory-Enabled HITL** (`email_assistant_hitl_memory.py`)
   - Adds persistent memory to learn from feedback

4. **Gmail Integration** (`email_assistant_hitl_memory_gmail.py`)
   - Connects to Gmail API for real email processing


## Running Tests

### Testing Scripts

Test to ensure all implementations work:

```bash
# Test all implementations
python tests/run_all_tests.py --all
```

(Note: This will leave out the Gmail implementation `email_assistant_hitl_memory_gmail` from testing.)

