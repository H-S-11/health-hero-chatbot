# HealthHero

A patient-aware RAG chatbot that combines **structured disease risk profiles**, **semantic retrieval**, and **LLM generation** to provide personalized health and lifestyle guidance.

HealthHero goes beyond generic chatbot responses by incorporating a patient's latest screening and risk information into the retrieval and generation pipeline.

> ⚠️ HealthHero is a decision-support prototype and does not provide medical diagnoses or replace healthcare professionals.

---

## How It Works

```text
Patient Question
       │
       ▼
Patient Context + Risk Profile
       │
       ▼
Risk Prioritization
       │
       ▼
RAG Retrieval ─────► ChromaDB
       │
       ▼
Relevant Knowledge + Patient Context
       │
       ▼
Gemini
       │
       ▼
Personalized Response
```

### Example

```text
Patient Risk Profile

Hypertension  → High
CVD           → Moderate
Stroke        → Moderate
Diabetes      → Low
CKD           → Low
```

If the patient asks:

> What should I eat?

HealthHero prioritizes relevant hypertension and cardiovascular knowledge before generating a personalized response.

---

## Key Features

- Patient-aware conversations using structured risk profiles
- Multi-condition risk prioritization
- Retrieval-Augmented Generation (RAG)
- Semantic search using ChromaDB
- Metadata-aware knowledge retrieval
- Personalized diet, lifestyle, and exercise guidance
- Modular FastAPI architecture
- Gemini-based LLM generation
- Reproducible knowledge-base ingestion
- Designed for web and WhatsApp integration

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | FastAPI |
| LLM | Google Gemini |
| Vector Database | ChromaDB |
| Embeddings | Sentence Transformers |
| Database | MongoDB |
| Knowledge Base | Markdown |
| Messaging | Twilio WhatsApp |

---

## Architecture

```text
Client
  │
  ▼
FastAPI
  │
  ▼
Chat Orchestrator
  │
  ├── Patient Context Service
  ├── Risk Prioritization
  ├── RAG Retrieval
  └── LLM Service
          │
          ▼
        Gemini
```

The system separates API handling, patient context, risk prioritization, retrieval, and LLM generation into independent services.

---

## Project Structure

```text
healthhero/
├── app/
│   ├── api/
│   │   └── chat.py
│   ├── services/
│   │   ├── chatbot_service.py
│   │   ├── patient_context_service.py
│   │   ├── risk_prioritization_service.py
│   │   ├── rag_service.py
│   │   └── gemini_service.py
│   └── main.py
│
├── knowledge_base/
├── scripts/
│   └── ingest_knowledge_base.py
│
├── requirements.txt
├── .env.example
└── README.md
```

---

## Getting Started

### Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/healthhero.git
cd healthhero
```

### Create a virtual environment

```bash
python -m venv venv
```

### Activate it

**Windows**

```bash
venv\Scripts\activate
```

**macOS/Linux**

```bash
source venv/bin/activate
```

### Install dependencies

```bash
pip install -r requirements.txt
```

### Configure environment variables

Create a `.env` file:

```env
GEMINI_API_KEY=your_api_key
MONGODB_URI=your_mongodb_uri
```

### Build the vector database

```bash
python -m scripts.ingest_knowledge_base
```

### Run the API

```bash
uvicorn app.main:app --reload
```

API documentation:

```text
http://localhost:8000/docs
```

---

## Example API Request

```json
POST /api/chat

{
  "patient_id": "demo_patient_001",
  "message": "What should I eat?"
}
```

### Example Response

```json
{
  "answer": "Based on the available screening profile, supporting healthy blood pressure and cardiovascular health should be prioritized.",
  "priority_conditions": [
    "hypertension",
    "cardiovascular",
    "stroke"
  ]
}
```

---

## Engineering Focus

HealthHero focuses on:

- Combining structured and unstructured data
- Context-aware retrieval
- Modular service architecture
- Reproducible RAG ingestion
- LLM provider isolation
- Controlled context construction
- Failure handling and safe responses

---

## Future Improvements

- Hybrid search and reranking
- Retrieval evaluation
- Conversation memory
- Redis caching
- Docker and CI/CD
- LLM provider fallback
- Multilingual support
- WhatsApp integration
- Source attribution

---

## Disclaimer

HealthHero is an educational and decision-support prototype. Disease risk scores are screening estimates and should not be interpreted as medical diagnoses.

Built as a modular conversational intelligence component for **Health Sense AI**.
