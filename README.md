# HCP Connect CRM – AI-First CRM for Life Sciences

An AI-powered CRM system for pharmaceutical field reps to log and manage Healthcare Professional (HCP) interactions using LangGraph + Groq AI.

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, Redux Toolkit, React Router |
| Backend | Python, FastAPI |
| AI Agent | LangGraph, LangChain |
| LLM | Groq – `gemma2-9b-it` |
| Database | SQLite (dev) / PostgreSQL (prod) |
| Font | Google Inter |

---

## 🤖 LangGraph Agent & 5 Tools

The LangGraph `create_react_agent` orchestrates a ReAct loop to process natural language from the sales rep and call the appropriate tool.

| # | Tool | Description |
|---|------|-------------|
| 1 | `log_interaction` | Logs a new HCP interaction with AI-generated summary |
| 2 | `edit_interaction` | Edits a specific field in an existing interaction |
| 3 | `get_hcp_history` | Retrieves past interaction history for an HCP |
| 4 | `suggest_follow_up` | Generates AI-powered next-best-action suggestions |
| 5 | `analyze_sentiment` | Classifies HCP sentiment from free-form text |

---

## 🚀 How to Run

### Prerequisites
- Python 3.10+
- Node.js 18+
- A free Groq API key from https://console.groq.com

---

### Step 1 – Get your Groq API Key
1. Go to https://console.groq.com
2. Sign up / log in
3. Click **API Keys** → **Create API Key**
4. Copy the key (starts with `gsk_...`)

---

### Step 2 – Set up the Backend

```bash
cd backend

# Create virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Set your Groq API key
# On Windows:
set GROQ_API_KEY=gsk_your_key_here
# On Mac/Linux:
export GROQ_API_KEY=gsk_your_key_here

# Start the backend
python main.py
```

Backend runs at: http://localhost:8000  
API docs at: http://localhost:8000/docs

---

### Step 3 – Set up the Frontend

Open a **new terminal**:

```bash
cd frontend

# Install dependencies
npm install

# Start the React app
npm start
```

Frontend opens at: http://localhost:3000

---

### Step 4 – Using the App

1. **Log Interaction (Form)**: Fill the left panel form with HCP details and click "Log Interaction"
2. **Log Interaction (Chat)**: Use the AI assistant on the right – describe an interaction in plain English
3. **History**: Click "History" in the nav to view, edit, or delete past interactions

---

### Demo Chat Commands (for video walkthrough)

Paste these into the chat box to demo all 5 tools:

```
# Tool 1 – log_interaction
Log a meeting with Dr. Anjali Sharma about Product X efficacy. She was interested and agreed to trial. Positive sentiment.

# Tool 2 – edit_interaction
Edit interaction 1, change sentiment to Positive

# Tool 3 – get_hcp_history
Get the interaction history for Dr. Anjali Sharma

# Tool 4 – suggest_follow_up
Suggest follow-up actions for Dr. Sharma after a positive meeting about efficacy data

# Tool 5 – analyze_sentiment
Analyze sentiment: The doctor was very enthusiastic and agreed to recommend our product to colleagues
```

---

## 📁 Project Structure

```
hcp-crm/
├── backend/
│   ├── main.py          # FastAPI app + all REST endpoints
│   ├── agent.py         # LangGraph agent + 5 tools
│   ├── requirements.txt
│   └── hcp_crm.db       # SQLite DB (auto-created on first run)
└── frontend/
    ├── public/
    │   └── index.html
    └── src/
        ├── App.js        # Root component + routing
        ├── App.css       # All styles
        ├── index.js      # Entry point
        ├── api/index.js  # Axios API calls
        ├── store/index.js # Redux store + slices
        └── pages/
            ├── LogInteractionPage.js   # Main CRM screen (form + chat)
            └── InteractionsListPage.js # History with edit/delete
```

---

## 🔑 Environment Variables

| Variable | Description |
|----------|-------------|
| `GROQ_API_KEY` | Your Groq API key (required for AI features) |

---

## 📝 Notes

- The SQLite database (`hcp_crm.db`) is created automatically in the backend folder
- 5 sample HCPs are pre-seeded for demo purposes
- The form and chat both save to the same database
- All 5 LangGraph tools are accessible via the chat interface
