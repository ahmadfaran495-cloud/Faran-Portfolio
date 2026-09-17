# FARAN // RE-ENTERING PRIME — Full-Stack AI Platform & Portfolio

An elite, high-performance personal portfolio website featuring a cinematic splash screen (*"Re-Entering Prime"*), a modular technical showcase, and a sovereign full-stack AI Chatbot powered by local Ollama instances with multi-session history, server-enforced rate limiting, and 100% mobile-responsive design.

---

## ⚡ Key Architectural Features

1. **Cinematic Splash Screen ("Re-Entering Prime")**:
   - Glitch title animation, cyberpunk scanline overlay, glowing radial energy pulse.
   - Real-time progress bar calibrating system parameters before transitioning into the portfolio.
   - Click-to-skip button (*"ENTER NOW →"*).

2. **Sovereign Local Ollama Integration**:
   - Zero cloud reliance: Connects directly to your local Ollama runtime on `http://127.0.0.1:11434`.
   - Dynamic model auto-detection (`/api/tags` and `/api/models`) supporting `llama3`, `mistral`, `deepseek-r1`, `phi3`, and `qwen2.5`.
   - Intelligent fallback simulation if Ollama isn't started yet, ensuring the portfolio is 100% testable out of the box.

3. **Multi-Session Chat History**:
   - Create new chat threads (`+ New Session`), switch between past conversations, and delete sessions.
   - Auto-saves locally in browser `localStorage` and persists on the backend in `data/history.json`.

4. **Sliding-Window Rate Limiter**:
   - Hardened backend middleware and client-side quota counter limiting queries to **20 requests per minute per IP**.
   - Sends standard HTTP `429 Too Many Requests` status, `Retry-After: 60`, and `X-RateLimit-*` headers when threshold is met.
   - Live visual fuel gauge in the sidebar.

5. **Rich Aesthetic & Mobile-Responsive Design**:
   - Curated **"Dominant Prime"** palette: Cyber Obsidian (`#07080c`), Electric Crimson (`#ff2e56`), and Prime Gold (`#ffb020`).
   - One-click theme switcher to **"Quantum Cyan"** (`#00f2fe`) & Hyper Violet (`#9055ff`).
   - Glassmorphism surfaces, responsive drawer navigation, touch-friendly chat interface, and floating action button (FAB).

6. **Interactive Retro Terminal**:
   - Built-in command line emulator in the contact section (`help`, `skills`, `ollama`, `about`, `theme`, `prime`, `clear`).

---

## 📁 Project Structure

```
e:\Faran's Projects\
├── index.html        # Main semantic markup, splash screen, portfolio & chat UI
├── style.css         # Complete CSS design system, glassmorphism & responsive styles
├── script.js         # Reactive client engine, Ollama bridge, chat state & rate-limiter
├── server.js         # Node.js backend (zero external dependencies required)
├── server.py         # Python backend (zero pip dependencies required)
├── package.json      # Node.js project metadata
├── requirements.txt  # Python metadata
├── start.bat         # Windows one-click launcher
├── start.ps1         # PowerShell launcher
├── README.md         # Documentation
└── data/
    └── history.json  # Persistent chat session store
```

---

## 🚀 Quick Start (Running Locally)

### Method 1: One-Click Windows Launcher (Recommended)
Simply double-click **`start.bat`** (or right-click `start.ps1` → *Run with PowerShell*).
The script will detect your environment, launch the backend server, and open the website in your default browser.

---

### Method 2: Running with Node.js
```bash
# In your terminal:
node server.js
```
The server will start on `http://localhost:3001` and automatically serve the frontend, API routes, and rate limiter. Open your browser to:
```
http://localhost:3001
```

---

### Method 3: Running with Python
```bash
# In your terminal:
python server.py
```
Open your browser to:
```
http://localhost:3001
```

---

### Method 4: Direct Browser Run (Standalone)
You can also directly double-click **`index.html`** in File Explorer to open it in Chrome, Edge, or Firefox.
The website's client engine will automatically probe for local services. If no backend is running, it operates in Sovereign Standby Demo Mode.

---

## 🧠 Connecting Local Ollama Models

1. **Install Ollama** from [ollama.com](https://ollama.com).
2. **Download and start your preferred model**:
   ```bash
   ollama run llama3
   ```
   *(Or `ollama run mistral`, `ollama run deepseek-r1:7b`)*
3. **Verify Ollama is listening**:
   Open `http://localhost:11434` in your browser. It should display:
   ```
   Ollama is running
   ```
4. **Refresh the website**:
   Click the refresh icon next to **Active Model** in the chat sidebar. The app will automatically detect your downloaded weights and populate the model dropdown!

---

## 🛡️ Rate Limiting Specification

- **Window**: 60 seconds (sliding window)
- **Quota**: 20 requests per IP address
- **Headers Returned**:
  - `X-RateLimit-Limit`: `20`
  - `X-RateLimit-Remaining`: Current tokens remaining
  - `Retry-After`: Seconds until quota replenishment
- **Status Code**: `HTTP 429 Too Many Requests`

---

## 🔒 Security & Privacy

- **Zero Third-Party Telemetry**: Queries never leave your local machine. All inference occurs on your local GPU/CPU via Ollama.
- **No API Keys or Secrets Exposed**: No hardcoded secrets, external SaaS tokens, or cloud deployments.
