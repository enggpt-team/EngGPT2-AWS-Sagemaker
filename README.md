# AWS SageMaker EngGPT2-16B-A3B Inference Guide

A practical guide for connecting to and querying the EngGPT2-16B-A3B model deployed on AWS SageMaker, with multiple inference modes including streaming, chat completions, and plain completions.

---

## Repository Structure

```
├── enggpt_guidelines_aws.ipynb       # Step-by-step guide for querying the model
├── requirements.txt     # Python dependencies
└── README.md
```

---

## Prerequisites

- Python 3.8+
- An AWS account with access to a deployed SageMaker endpoint
- Valid AWS credentials: Access Key, Secret Key, and Session Token

---

## Installation

Install the required dependencies:

```bash
pip install -r requirements.txt
```

---

## Configuration

The notebook connects to the SageMaker runtime using your AWS credentials. Before running the notebook, set up your environment variables in a `.env` file at the root of the repository:

```env
AWS_ACCESS_KEY=your_access_key_here
AWS_SECRET_KEY=your_secret_key_here
AWS_SESSION_TOKEN=your_session_token_here
```

The client is initialized as follows:

```python
import boto3
from dotenv import load_dotenv
import os

load_dotenv()

runtime = boto3.client(
    'sagemaker-runtime',
    aws_access_key_id=os.getenv("AWS_ACCESS_KEY"),
    aws_secret_access_key=os.getenv("AWS_SECRET_KEY"),
    aws_session_token=os.getenv("AWS_SESSION_TOKEN"),
    region_name='eu-central-1'
)
```

---

## Notebook Overview

The notebook (`enggpt_guidelines_aws.ipynb`) covers the following inference modes:

### Chat Completions
Send a structured conversation history to the model (system + user messages) and receive a complete response. Supports both English and Italian input.

### Plain Completions
Send a raw text prompt and receive a direct completion from the model, without conversation context.

### Streaming
Query the model with streaming enabled to receive the response token by token in real time. Available for both chat and plain completion modes.

### Reasoning Modes
The notebook demonstrates different reasoning configurations that affect how the model processes and responds to queries.

### Language Support
Examples are provided in both **English** (`en`) and **Italian** (`ita`).

---

## Dependencies

| Package | Purpose |
|---|---|
| `boto3` | AWS SDK for Python — connects to SageMaker runtime |
| `python-dotenv` | Loads environment variables from a `.env` file |
