# VOCA AI

**Multilingual Conversation Intelligence Platform**

---

## Overview

VOCA AI is an API-first, enterprise-grade conversation intelligence backend that analyzes multilingual customer interactions (voice or text) and generates structured, configurable insights.

It is designed for real-world integration into **banking**, **telecom**, **insurance**, and **customer support** systems.

The system processes conversations and extracts:

- Business domain-aware summary
- Language detection (multilingual)
- Sentiment & emotional tone
- Customer intent detection
- Key topics/entities
- Risk & escalation scoring
- Compliance & policy violations
- Agent performance insights

---

## Architecture

```
User Input (Text / Audio)
        ↓
Speech-to-Text (Whisper GPU – for audio)
        ↓
Conversation Structuring (Speaker Parsing)
        ↓
LLM Analysis (Groq LLaMA 3.1)
        ↓
Client-Config Driven Analysis Layer
        ↓
Guardrail & Compliance Engine
        ↓
Risk Engine (Explainable Risk Score)
        ↓
Structured Enterprise JSON Output
```

---

## AI Usage Approach

### 1️⃣ Large Language Model (Groq LLaMA 3.1)

**Used for:**

- Domain-aware summary generation
- Multilingual detection
- Sentiment & emotion detection
- Intent classification
- Topic extraction
- Call outcome classification
- Agent behavior analysis

The LLM is influenced dynamically by client configuration context.

### 2️⃣ Whisper (GPU Accelerated)

**Used for:**

- Audio transcription
- Primary language detection
- Multilingual support

**Model configuration:**

```python
WhisperModel("medium", device="cuda", compute_type="float16")
```

### 3️⃣ Hybrid Guardrail & Risk Engine

Rule-based detection layered on top of AI analysis:

- Offensive language detection
- Legal/regulatory threat detection
- Policy violation detection
- Out-of-scope conversation
- Escalation keywords
- Risk multiplier logic

Risk score is **explainable**:

```json
"risk_assessment": {
  "score": 85,
  "level": "High",
  "factors": [
    "RBI escalation threat",
    "High emotional intensity",
    "Policy violation detected"
  ]
}
```

---

## Configurable Client Context (Mandatory Requirement)

The system supports **client-defined configuration** that influences analysis.

### Example Input

```json
{
  "text": "Customer: I will complain to RBI if this is not resolved.",
  "client_config": {
    "domain": "Banking",
    "products": ["Home Loan", "Credit Card"],
    "policies": ["Escalation handling", "KYC mandatory"],
    "risk_triggers": ["RBI", "legal action", "consumer court"]
  }
}
```

### How It Influences Analysis

| Aspect | Influence |
|--------|-----------|
| **Domain** | Biasing in summary & intent detection |
| **Risk** | Score adjusted based on custom triggers |
| **Compliance** | Engine uses client policies |
| **Output** | Adapts to enterprise context |

This satisfies the **Configurable Client Context** requirement.

---

## API Endpoints

### 1️⃣ `POST /api/analyze/text`

Analyzes structured or plain-text conversation.

**Request Body**

```json
{
  "text": "Customer: My card was charged twice.\nAgent: Let me check.\nCustomer: I will escalate this legally.",
  "client_config": {
    "domain": "Banking",
    "products": ["Credit Card"],
    "policies": ["Escalation policy"],
    "risk_triggers": ["legal", "RBI", "complaint"]
  }
}
```

### 2️⃣ `POST /api/analyze/audio`

Accepts audio file and performs:

- Speech-to-text
- Language detection
- Full conversation analysis

---

## Sample Response

```json
{
  "detected_domain": "Banking",
  "summary": "Customer reports double charge and threatens legal escalation.",
  "language": ["English"],
  "sentiment": "Negative",
  "emotion": "Frustrated",
  "emotion_intensity": "High",
  "intents": ["Refund request", "Escalation"],
  "topics": ["Credit card", "Double charge"],
  "agent_analysis": {
    "professionalism": "Moderate",
    "resolution_effectiveness": "Pending"
  },
  "compliance_issues": [
    {
      "type": "Escalation Threat",
      "severity": "High"
    }
  ],
  "risk_assessment": {
    "score": 82,
    "level": "High",
    "factors": [
      "Legal escalation language",
      "High emotional intensity"
    ]
  },
  "call_outcome": "Escalation Likely"
}
```

---

## Installation & Setup

### 1️⃣ Clone Repository

```bash
git clone https://github.com/your-repo/voca_ai.git
cd voca_ai
```

### 2️⃣ Create Virtual Environment

```bash
python -m venv venv
source venv/bin/activate   # Mac/Linux
venv\Scripts\activate      # Windows
```

### 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

### 4️⃣ Configure Environment Variables

Create `.env` file:

```env
GROQ_API_KEY=your_api_key_here
HF_HUB_DISABLE_SYMLINKS_WARNING=1
```

### 5️⃣ Run Server

```bash
uvicorn app.main:app --reload
```

**Access Swagger Docs:** [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## Advanced Analysis Implemented

| Feature | Status |
|---------|--------|
| Compliance violation detection | ✔ |
| Risk & escalation scoring | ✔ |
| Agent quality evaluation | ✔ |
| Call outcome classification | ✔ |
| Multilingual detection | ✔ |
| Timeline-ready architecture | ✔ |

---

## Limitations

- **Manglish/Hinglish** detection depends on transliteration accuracy
- **Whisper** accuracy depends on audio clarity
- **Risk scoring** uses heuristic multiplier logic
- No real-time streaming yet
- No persistent database storage

---

## Future Improvements

- Real-time streaming analysis
- Emotion timeline visualization API
- Agent numeric performance scoring (0–100)
- Escalation probability ML model
- Vector database for historical insights
- RAG-based compliance rule matching
- Multi-tenant config database

---

## Enterprise Readiness

| Criterion | Status |
|-----------|--------|
| API-first architecture | ✔ |
| Clean request/response schemas | ✔ |
| Configurable client context | ✔ |
| Multimodal input | ✔ |
| Explainable risk scoring | ✔ |
| Guardrail governance | ✔ |
| Production-ready structure | ✔ |
| Hackathon requirement compliant | ✔ |
