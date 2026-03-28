# ✦ ARIA — Personal AI Agent

A full-stack personal AI agent built with vanilla HTML/CSS/JS and the Anthropic Claude API. Features a real-time chat interface, Gmail-style inbox with AI summaries, weekly calendar view, and a long-term memory system.

![ARIA Screenshot](docs/screenshot.png)

## Features

- **AI Chat** — Powered by Claude Sonnet. Context-aware of your inbox, calendar, and memory. Full conversation history maintained per session.
- **Inbox** — Email list with AI-generated summaries, priority tagging (high/medium/low), and one-click "Draft Reply with AI" actions.
- **Calendar** — Week-grid view with event rendering. Natural language quick-add (e.g. "Standup tomorrow 9am").
- **Memory** — Long-term knowledge base: preferences, projects, contacts, and context cards that ARIA uses to personalize responses.
- **Tool Simulation** — ARIA describes using `read_email`, `schedule_event`, `search_memory`, `web_search` tools naturally in conversation.

## Stack

```
Frontend:   Vanilla HTML + CSS + JavaScript (zero dependencies)
AI:         Anthropic Claude API (claude-sonnet-4-20250514)
Fonts:      DM Mono + DM Sans (Google Fonts)
Deploy:     Any static host — GitHub Pages, Vercel, Netlify, Cloudflare Pages
```

## Project Structure

```
aria-agent/
├── index.html              # Entry point (single-file app)
├── src/
│   ├── components/
│   │   ├── chat.js         # Chat view logic + API calls
│   │   ├── email.js        # Inbox rendering + actions
│   │   ├── calendar.js     # Week grid + event rendering
│   │   └── memory.js       # Memory cards rendering
│   ├── utils/
│   │   ├── api.js          # Anthropic API wrapper
│   │   ├── data.js         # Mock data (emails, events, memories)
│   │   └── helpers.js      # Shared utility functions
│   └── styles/
│       └── main.css        # All styles (extracted from index.html)
├── public/
│   └── favicon.svg         # ARIA favicon
├── docs/
│   ├── ARCHITECTURE.md     # System design & decisions
│   └── EXTENDING.md        # How to add real Gmail/Calendar APIs
├── .env.example            # Environment variable template
├── .gitignore
└── README.md
```

## Quick Start

### 1. Clone the repo

```bash
git clone https://github.com/YOUR_USERNAME/aria-agent.git
cd aria-agent
```

### 2. Set your API key

This project calls the Anthropic API from the browser. For local development:

```bash
cp .env.example .env
# Edit .env and add your ANTHROPIC_API_KEY
```

> **Note:** The standalone `index.html` calls the API directly from the browser (no backend needed). This works on Claude.ai. For production, use the backend proxy approach described in `docs/EXTENDING.md`.

### 3. Run locally

```bash
# Option A: Python (no install needed)
python3 -m http.server 8080

# Option B: Node.js
npx serve .

# Option C: Just open index.html in your browser
open index.html
```

### 4. Deploy

**GitHub Pages:**
```bash
git push origin main
# Enable Pages in repo Settings → Pages → Deploy from branch: main
```

**Vercel:**
```bash
npx vercel --prod
```

**Netlify:**
```bash
npx netlify deploy --prod --dir .
```

## Configuration

Edit `src/utils/data.js` to customize:
- Your email mock data
- Calendar events
- Memory / context cards
- ARIA's system prompt (in `src/utils/api.js`)

## Extending with Real APIs

See `docs/EXTENDING.md` for step-by-step guides on connecting:
- **Gmail API** (Google OAuth + Gmail REST API)
- **Google Calendar API**
- **Notion API** (for memory/notes)
- **Backend proxy** (to keep your API key server-side)

## Architecture

```
Browser
  └── index.html
        ├── Renders UI (chat, inbox, calendar, memory)
        ├── src/components/*.js  ← view logic
        ├── src/utils/api.js     ← Claude API calls
        └── src/utils/data.js    ← mock data layer

API Layer
  └── POST https://api.anthropic.com/v1/messages
        ├── model: claude-sonnet-4-20250514
        ├── system: context-aware prompt
        └── messages: full conversation history
```

## Roadmap

- [ ] Real Gmail OAuth integration
- [ ] Real Google Calendar sync
- [ ] Persistent memory (localStorage → Supabase)
- [ ] Streaming responses (SSE)
- [ ] Voice input (Web Speech API)
- [ ] Notion / Obsidian integration
- [ ] Mobile PWA support

## License

MIT — do whatever you want with it.

---

Built with ✦ and [Claude](https://anthropic.com)
