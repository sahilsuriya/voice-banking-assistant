# AI Voice Assistant for Financial Operations

This project is a Proof-of-Concept (POC) AI-powered Voice Banking Assistant built using **Rasa NLU**, **FastAPI**, and a lightweight **HTML/CSS/JavaScript frontend**.

The assistant allows users to perform mock financial operations using natural language voice commands while keeping conversations private through a self-hosted open-source NLP pipeline.

---

# Features

- Voice-based banking assistant
- Speech-to-Text using Browser Web Speech API
- Text-to-Speech responses
- Secure intent recognition using Rasa NLU
- Mock financial operations
- Multi-step conversational flow
- FastAPI backend for banking logic
- Privacy-focused architecture
- No third-party NLP APIs

---

# Tech Stack

| Component | Technology |
|------------|-------------|
| Frontend | HTML, CSS, JavaScript |
| Backend | FastAPI |
| NLU Engine | Rasa NLU |
| Voice Input | Web Speech API |
| Voice Output | Speech Synthesis API |
| Server | Uvicorn |

---

# Project Architecture

```text
User Voice
   │
   ▼
Frontend (Browser UI)
   │
   ▼
FastAPI Backend
   │
   ▼
Rasa NLU Engine
   │
   ▼
Intent + Entities
   │
   ▼
Backend Banking Logic
   │
   ▼
Frontend Voice Response
```

---

# Project Structure

```text
AGENT/
├── .gitignore
├── README.md
├── main.py                     # FastAPI Backend
│
├── frontend/                   # Frontend Web Application
│   ├── index.html
│   ├── script.js
│   └── style.css
│
├── rasa_agent/                 # Rasa NLU Service
│   ├── config.yml
│   ├── domain.yml
│   ├── data/
│   │   └── nlu.yml
│   └── models/
│       └── nlu-....tar.gz
│
└── venv-rasa/                  # Python Virtual Environment
```

---

# How It Works

The project consists of three separate services:

## 1. Frontend (The Face)

The frontend is responsible for:

- Capturing user voice
- Converting speech to text
- Sending requests to the backend
- Displaying assistant responses
- Speaking responses using text-to-speech

### Technologies Used

- HTML
- CSS
- JavaScript
- Web Speech API

---

## 2. Backend (The Conductor)

The FastAPI backend acts as the orchestrator between the frontend and the Rasa NLU engine.

### Responsibilities

- User authentication
- Session management
- Banking operations
- Communicating with Rasa NLU
- Returning responses to the frontend

### Example Operations

- Check balance
- View transaction history
- Transfer money
- Cash inquiries

---

## 3. Rasa NLU (The Brain)

Rasa processes user messages and extracts:

- Intent
- Entities

### Example

User says:

```text
Send 50 dollars to Jane
```

Rasa extracts:

```json
{
  "intent": "transfer_money",
  "entities": {
    "amount": "50",
    "recipient": "Jane"
  }
}
```

---

# Prerequisites

Before running the project, ensure you have:

- Python 3.10 or Python 3.11
- pip
- Python virtual environment
- Google Chrome or Microsoft Edge browser

> Note: Python 3.12+ is NOT supported due to Rasa/TensorFlow compatibility issues.

---

# Installation

## Step 1: Clone the Repository

```bash
git clone <your-repository-url>
cd AGENT
```

---

## Step 2: Create Virtual Environment

### Windows

```bash
py -3.10 -m venv venv-rasa
```

### Activate Virtual Environment

```bash
.\venv-rasa\Scripts\activate
```

---

## Step 3: Install Dependencies

```bash
pip install rasa fastapi "uvicorn[standard]" pydantic httpx
```

---

# Train the Rasa NLU Model

Navigate into the `rasa_agent` directory:

```bash
cd rasa_agent
```

Train the model:

```bash
rasa train nlu
```

Return to the root directory:

```bash
cd ..
```

---

# Running the Project

You must run all three services simultaneously in separate terminals.

---

# Terminal 1 — Start Rasa NLU Server

Open Terminal 1:

```bash
.\venv-rasa\Scripts\activate
cd rasa_agent
rasa run -m models --enable-api
```

The Rasa server will run on:

```text
http://localhost:5005
```

---

# Terminal 2 — Start FastAPI Backend

Open Terminal 2:

```bash
.\venv-rasa\Scripts\activate
uvicorn main:app --reload
```

The backend server will run on:

```text
http://localhost:8000
```

---

# Terminal 3 — Start Frontend Server

Open Terminal 3:

```bash
cd frontend
python -m http.server 8001
```

The frontend will run on:

```text
http://localhost:8001
```

---

# Usage

Open your browser and navigate to:

```text
http://localhost:8001
```

Allow microphone permissions when prompted.

---

# Demo Login Credentials

```text
Username: user123
Password: password123
```

---

# Example Voice Commands

## Balance Inquiry

```text
"What is my balance?"
```

```text
"Show me my cash."
```

---

## Transaction History

```text
"What's my transaction history?"
```

---

## Money Transfer

```text
"I want to send money."
```

```text
"Send 50 dollars to Jane."
```

---

# Example Conversation Flow

```text
User: Send money
Bot: Sure, how much would you like to send?
User: 50 dollars
Bot: Who would you like to send it to?
User: Jane
Bot: Successfully transferred 50 dollars to Jane.
```

---

# API Communication Flow

```text
Frontend
   │
   ▼
POST /chat
   │
   ▼
FastAPI Backend
   │
   ▼
POST /model/parse
   │
   ▼
Rasa NLU
   │
   ▼
Intent + Entities
   │
   ▼
Business Logic
   │
   ▼
Frontend Response
```

---

# Security & Privacy

This project prioritizes user privacy and local processing.

## Privacy Benefits

- No OpenAI APIs
- No external NLP providers
- Self-hosted intent recognition
- Local conversation processing
- User voice data remains local

---

# Sample Intents

| Intent | Description |
|--------|-------------|
| check_balance | Check account balance |
| transaction_history | View transaction history |
| transfer_money | Transfer money |
| greet | Greeting |
| goodbye | End conversation |

---

# Future Improvements

- Real banking API integration
- JWT authentication
- Database support
- Redis caching
- Multi-language support
- Voice biometrics
- OTP verification
- Docker deployment
- Kubernetes deployment
- Fraud detection system
- LLM integration for advanced conversations

---

# Troubleshooting

## Rasa Server Not Starting

Check your Python version:

```bash
python --version
```

Use Python 3.10 or 3.11 only.

---

## Microphone Not Working

- Use Chrome or Edge browser
- Allow microphone permissions
- Use HTTPS in production

---

## Frontend Cannot Reach Backend

Ensure:

- Backend is running on port 8000
- Rasa server is running on port 5005
- No firewall is blocking ports

---

# Development Notes

This project was built as a Proof-of-Concept for the:

```text
AI Voice Assistant for Financial Operations Challenge
```

The project demonstrates:

- Conversational AI
- Voice interfaces
- Secure NLP systems
- Financial operation automation

---

# License

This project is intended for educational and demonstration purposes.

---

# Author

Developed for the:

```text
AI Voice Assistant for Financial Operations
```

challenge.
