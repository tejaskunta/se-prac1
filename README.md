# PrivacyShield.AI / securAI

Team: **CodeRed**  
Technologies: **FastAPI, Presidio, spaCy, Gemini API, MongoDB, React + Vite, Material UI**

---

## 📦 Project Structure

```
├── backend/
│   ├── main.py              # FastAPI app with /v1/analyze, /v1/sample, /health
│   ├── gemini_client.py     # Call Gemini generativelanguage API
│   ├── privacy_engine.py    # Presidio Analyzer + Anonymizer (fallback regex)
│   ├── db.py                # MongoDB async (motor)
│   ├── models.py            # Pydantic models
│   ├── utils.py             # compute_privacy_score
│   ├── requirements.txt     # Python deps
│   ├── .env.example         # Required env vars
│   └── public/sample.json   # Static fallback data
├── frontend/
│   ├── src/
│   │   ├── main.jsx         # React entry
│   │   ├── App.jsx          # Main app component
│   │   ├── api.js           # Axios wrapper
│   │   ├── PromptForm.jsx   # User input + submit
│   │   ├── ResultPanel.jsx  # Display results
│   │   ├── EntityHighlighter.jsx  # Highlight entities with fallback validation
│   │   ├── PrivacyScoreBar.jsx    # Color-coded linear bar
│   │   └── HistoryTable.jsx       # localStorage history (max 20)
│   ├── public/sample.json   # Offline fallback
│   ├── index.html           # HTML entry point
│   ├── vite.config.js       # Vite + React plugin
│   ├── package.json         # NPM dependencies
│   └── .env                 # VITE_API_URL=http://localhost:8000
└── README.md (this file)
```

---

## 🚀 Quick Start

### Backend

```bash
cd backend
pip install -r requirements.txt
python -m spacy download en_core_web_lg

# Copy .env.example to .env and fill in GEMINI_API_KEY
cp .env.example .env

# Start server
uvicorn main:app --reload
```

Visit: <http://localhost:8000/health>

### Frontend

```bash
cd frontend
npm install
npm run dev
```

Visit: <http://localhost:5173>

---

## 🔑 Environment Variables (Backend .env)

```bash
MONGO_URI=mongodb://localhost:27017
MONGO_DB=securai
GEMINI_API_KEY=YOUR_KEY
GEMINI_MODEL=gemini-pro
GEMINI_API_URL=https://generativelanguage.googleapis.com/v1beta/models
PORT=8000
ALLOW_ORIGINS=http://localhost:5173
```

---

## 📡 API Endpoints

| Endpoint         | Method | Description                                         |
|------------------|--------|-----------------------------------------------------|
| `/health`        | GET    | Health check                                        |
| `/v1/analyze`    | POST   | Analyze text, redact PII, call Gemini, return JSON |
| `/v1/sample`     | GET    | Static sample data (offline fallback)               |

**POST /v1/analyze** Request:

```json
{
  "text": "string"
}
```

Response:

```json
{
  "original_text": "...",
  "redacted_text": "...",
  "entities": [{"type":"EMAIL","start":0,"end":10}],
  "privacy_score": 33,
  "gemini_response": "..."
}
```

---

## 🛡 Privacy Pipeline

1. User enters prompt in frontend
2. Frontend sends POST to backend `/v1/analyze`
3. Backend analyzes using **Presidio + spaCy**
4. Backend redacts sensitive entities
5. **ONLY REDACTED TEXT** is sent to Gemini
6. Backend returns original + redacted + entities + score + Gemini response
7. Frontend highlights entities + displays score + Gemini output
8. Backend logs (timestamp, score, entity_types) → MongoDB (no raw PII)
9. Frontend persists last 20 redacted prompts to localStorage (no raw PII)

---

## 🧪 Testing

**Backend**: Visit <http://localhost:8000/health> and <http://localhost:8000/v1/sample>

**Frontend**: If backend is down, frontend automatically fetches `/sample.json` and displays an offline warning.

---

## 🚢 Deployment

### Frontend (Vercel)

Deploy the `frontend/` folder. Set environment variable:

```
VITE_API_URL=https://your-backend-url
```

### Backend (Railway / Render / Google Cloud Run / Azure Container Apps / AWS ECS)

- Set all env vars from `.env.example`
- Ensure CORS allows your frontend domain
- Install spaCy model: `python -m spacy download en_core_web_lg`

---

## 📝 Coding Rules

- **YAGNI**: Only features needed for demo
- **KISS**: Short functions (20–40 lines), one responsibility per file
- **DRY**: Single source of truth for redaction logic

---

## 📚 Tech Docs

- [FastAPI](https://fastapi.tiangolo.com/)
- [Presidio](https://microsoft.github.io/presidio/)
- [spaCy](https://spacy.io/)
- [Gemini API](https://ai.google.dev/docs)
- [MongoDB Motor](https://motor.readthedocs.io/)
- [Vite](https://vitejs.dev/)
- [Material UI](https://mui.com/)

---

## 👥 Team CodeRed

Built for **GitHub Copilot / VS Code Agents** use.

# se-prac1
