# LLM Prompt Router for Intent Classification

## Overview

This project implements an **LLM-powered prompt routing system** that classifies user intent and routes the request to a specialized AI persona. Instead of using a single large prompt, the system first detects the user's intent and then delegates the request to an expert prompt designed for that task.

This architecture improves response quality, efficiency, and modularity for real-world AI applications.

---

## Features

* Intent classification using an LLM
* Prompt routing to specialized AI personas
* Four expert personas:

  * Code Expert
  * Data Analyst
  * Writing Coach
  * Career Advisor
* Clarification handling for unclear queries
* Structured JSON logging of all requests
* Docker containerization
* Command-line interface (CLI)

---

## System Architecture

The system follows a **two-step LLM pipeline**:

1. **Intent Classification**

   * A lightweight prompt determines the user's intent.
   * The model returns a structured JSON response.

2. **Prompt Routing**

   * The system selects the appropriate expert prompt.
   * The user request is routed to that expert for response generation.

```
User Input
     │
     ▼
Intent Classifier (LLM)
     │
     ▼
Intent Label + Confidence
     │
     ▼
Prompt Router
     │
     ├── Code Expert
     ├── Data Analyst
     ├── Writing Coach
     ├── Career Advisor
     └── Clarification Handler
     │
     ▼
Final Response
```

---

## Project Structure

```
llm-prompt-router
│
├── classifier.py          # Intent classification logic
├── router.py              # Routing and response generation
├── prompts.py             # Expert system prompts
├── logger.py              # Request logging system
├── main.py                # CLI interface
│
├── Dockerfile             # Docker container configuration
├── docker-compose.yml     # Docker orchestration
│
├── route_log.jsonl        # Request logs
├── .env.example           # Environment variables template
├── .gitignore             # Ignored files
└── README.md              # Project documentation
```

---

## Environment Variables

Create a `.env` file based on `.env.example`.

Example:

```
OPENROUTER_API_KEY=your_api_key_here
```
---

## Installation

Clone the repository:

```
git clone https://github.com/Swetha-svvv/LLM-Prompt-Router.git
cd llm-prompt-router
```

Install dependencies:

```
pip install -r requirements.txt
```

---

## Running the Application

Run the CLI interface:

```
python main.py
```

Example:

```
Enter message: how do I sort a list in python

Detected Intent: code
Confidence: 0.9
```

---

## Running with Docker

Build and start the container:

```
docker-compose up --build
```

Run the application interactively:

```
docker run -it llm-prompt-router-prompt-router
```

---

## Logging

All requests are logged to:

```
route_log.jsonl
```

Each log entry contains:

```
{
  "intent": "code",
  "confidence": 0.9,
  "user_message": "how do I sort a list in python",
  "final_response": "..."
}
```

This allows tracking routing decisions and responses.

---

## Example Test Cases

| Input                                                | Detected Intent |
| ---------------------------------------------------- | --------------- |
| how do I sort a list in python                       | code            |
| what's the average of 12,45,23,67                    | data            |
| this paragraph sounds awkward can you help me fix it | writing         |
| i am preparing for a job interview                   | career          |
| hey                                                  | unclear         |

---

## Core Requirements Implemented

* Multiple expert prompts
* LLM-based intent classification
* Intent-based prompt routing
* Clarification handling
* Structured JSON logging
* Docker containerization

---

## Technologies Used

* Python
* LLM API (OpenRouter / LLaMA / Gemini)
* Docker
* JSON logging
* Prompt Engineering

---

## Future Improvements

* Web interface using FastAPI or Flask
* Confidence threshold filtering
* Manual intent override (e.g., `@code`)
* Advanced analytics for routing logs

---

## Author

**Swetha**
