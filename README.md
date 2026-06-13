# NEXUS — Civilization Collapse Engine

> *Eight extinction-level threats. Real scientific data. Every decision reshapes humanity's probability of survival.*

[![Live Demo](https://img.shields.io/badge/Live%20Demo-GitHub%20Pages-blue?style=flat-square)](https://AshQ-ghbi.github.io/Nexus)
[![Hackathon](https://img.shields.io/badge/Microsoft%20Innovation%20Studio-Creative%20Apps-purple?style=flat-square)](https://innovationstudio.microsoft.com)
[![Built with Copilot](https://img.shields.io/badge/Built%20with-GitHub%20Copilot-black?style=flat-square&logo=github)](https://github.com/features/copilot)
[![AI Engine](https://img.shields.io/badge/AI%20Engine-Claude%20(Anthropic)-orange?style=flat-square)](https://www.anthropic.com)

---

## What is NEXUS?

NEXUS is a **cinematic, AI-powered civilization collapse simulator** built for the [Microsoft - Agents League Hackathon](https://innovationstudio.microsoft.com) under the **Creative Apps** track.

It transforms real-world scientific and geopolitical data into an interactive decision-making engine — asking a single terrifying question:

> **What kills humanity first, and what can we do about it?**

Players choose from **8 extinction-level threat scenarios** — each grounded in data from NASA, WHO, SIPRI, RAND Corporation, and more. Every intervention decision shifts a live civilization survival percentage, and the AI analyzes each choice with context drawn from the player's full decision history via a **Work IQ–inspired memory layer**.

---

## Tabs

| Home Screen | Threat Matrix | Simulator | Decision Memory |
|---|---|---|---|
| Survival ring + doomsday clock + radar chart | 8 threats with risk levels + intel feed | Timeline + decisions + AI analysis | Work IQ persistent memory |

---

## Features

### 🌍 Home Screen
- Live scrolling **threat ticker** with real-world headlines
- **Survival ring** with 3-color gradient (red → amber → green) and session delta
- **Doomsday Clock** counting down to year-end midnight
- **Canvas-drawn radar chart** visualizing all 8 threat vectors simultaneously
- Animated background grid

### ⚠️ Threat Matrix
- **8 collapse scenarios** with individual risk indices
- Stat strip: average global threat level + active flashpoints counter
- Horizontal probability breakdown bar for all 8 threats
- **Intel Feed** — 6 real-world-style news items, each tagged and timestamped

### 🔬 Simulator
- Per-threat **intelligence data panel** (casualties, risk index, classification, data sources)
- **Timeline** with PAST / NOW / PROJECTED markers
- **Critical Decision** module with 4 intervention options per scenario
- Live survival meter with collapse threshold line at 15%
- **AI analysis** via Claude API — context-aware, Work IQ memory injected into every prompt
- Fallback responses when API unavailable

### 🧠 Decision Memory (Work IQ Layer)
- Persistent `localStorage`-based decision storage across sessions
- Total decisions counter + positive outcome ratio
- Full decision history with survival impact per choice
- **Work IQ context injection** — last 3 decisions sent with every AI prompt

### 🏆 Leaderboard
- Global player count + average survival rate stats
- Player avatar initials with color coding
- Your score inserted dynamically into global rankings

### ℹ️ About
- Full hackathon track alignment details
- Per-threat data source breakdown table
- Complete tech stack listing

---

## Work IQ Intelligence Layer

Every submission to the Microsoft Innovation Studio Hackathon must integrate at least one Microsoft IQ intelligence layer.

NEXUS integrates a **Work IQ–inspired personal memory system** that mirrors how Work IQ operates in Microsoft 365 Copilot:

| Work IQ (Microsoft) | NEXUS Implementation |
|---|---|
| Builds context from emails, meetings, documents | Builds context from every decision made in simulations |
| Personalizes Copilot responses to your work patterns | Personalizes AI analysis to your behavioral archetype |
| Remembers relationships and recurring topics | Remembers which threats you've faced and how you responded |
| Surfaces relevant context automatically | Injects last 3–5 decisions into every Claude API prompt |

```javascript
// Work IQ context injection — every AI prompt includes decision history
const prev = state.memory.slice(1, 4)
  .map(m => `${m.threatName}: "${m.choice.substring(0, 50)}" (${m.delta > 0 ? '+' : ''}${m.delta}%)`)
  .join(' | ');

const prompt = `... Player's decision history: ${prev || 'First decision'} ...`;
```

---

## Threat Scenarios

| # | Threat | Risk Index | Tag | Data Sources |
|---|---|---|---|---|
| 1 | 🤖 AI Singularity | 88% | EXTREME | RAND Corp, Alignment Forum, ARC Evals |
| 2 | 🌊 Climate Cascade | 74% | HIGH | NASA Earth Observatory, NOAA, IPCC AR6 |
| 3 | ☢️ Nuclear Winter | 61% | CRITICAL | SIPRI Yearbook 2024, Bulletin of Atomic Scientists |
| 4 | 🦠 Engineered Pandemic | 69% | HIGH | WHO, Johns Hopkins CSSE, Our World in Data |
| 5 | 💹 Economic Black Hole | 52% | MODERATE | IMF World Economic Outlook, World Bank, IIF |
| 6 | 💻 Cyber Collapse | 58% | HIGH | CISA, Mandiant Threat Report 2024, CrowdStrike |
| 7 | 🪨 Asteroid Impact | 21% | LOW | NASA CNEOS, ESA NEOCC, B612 Foundation |
| 8 | ☀️ Solar Superstorm | 44% | MODERATE | NOAA SWPC, Royal Academy of Engineering |

---

## Tech Stack

```
Frontend:    Vanilla HTML5, CSS3, JavaScript — zero frameworks
AI Engine:   Anthropic API
IQ Layer:    Work IQ simulation — localStorage + AI prompt injection
Dev Tool:    GitHub Copilot in VS Code (Creative Apps track requirement)
Charts:      HTML5 Canvas API (radar chart)
Hosting:     GitHub Pages
Typography:  Orbitron · Space Grotesk · JetBrains Mono (Google Fonts)
```

---

## Hackathon Alignment

| Field | Value |
|---|---|
| **Event** | Microsoft Innovation Studio Hackathon |
| **Track** | Creative Apps |
| **Primary Tool** | GitHub Copilot (VS Code) |
| **IQ Layer** | Work IQ (personal memory & context persistence) |
| **AI Engine** | Claude via Anthropic API |
| **Platform** | GitHub Pages |

### Why Creative Apps?

NEXUS is a creative, visually rich, interactive experience that could not exist without AI-assisted development — both in code generation (Copilot) and runtime intelligence (Claude API + Work IQ layer). GitHub Copilot was used to:

- Scaffold the multi-page navigation system
- Generate threat timeline data structures
- Write the Work IQ memory layer logic
- Accelerate the Canvas radar chart implementation
- Build the CSS animation system

Estimated development time reduction: **~70%**

---

## Setup & Deployment

### GitHub Pages :

```bash
# 1. Fork or clone this repository
git clone https://github.com/your-username/nexus.git
cd nexus

# 2. Enable GitHub Pages in repository settings
# Settings → Pages → Source: Deploy from main branch / root

# 3. Visit https://your-username.github.io/nexus
```

The app is a **single HTML file** with zero build steps, zero dependencies, and zero configuration required.

### API Key (Optional)

The Claude AI analysis works **without an API key** — fallback responses are built in. To enable live AI analysis:

The app calls `https://api.anthropic.com/v1/messages` directly from the browser. For a production deployment, you should proxy this through a backend to protect your API key.

For hackathon/demo purposes, the fallback responses are high-quality and cover all decision archetypes.

---

## Project Structure

```
nexus/
├── index.html          # Complete single-file application
├── README.md           # This file
├── docs/
│   ├── ARCHITECTURE.md # Technical deep-dive
│   └── WORK_IQ.md      # Work IQ integration documentation
└── assets/             # (screenshots, diagrams)
```

---

## Design Philosophy

NEXUS uses a **cinematic dark-ops aesthetic** — inspired by real intelligence dashboards, crisis operations centers, and science fiction command interfaces.

**Typography:**
- `Orbitron` — futuristic monospaced display for titles and numbers
- `Space Grotesk` — humanist sans for body text and decisions
- `JetBrains Mono` — developer mono for data labels and system text

**Color System:**
- Each of the 8 threats has a unique accent color
- Survival ring uses a 3-stop gradient: danger red → warning amber → safe green
- Background uses layered dark blues with scanline overlay for depth

**Motion:**
- Animated grid background on home screen
- Smooth survival bar transitions (1.2s cubic-bezier)
- Ticker tape with pause-on-hover
- Page transition fade-in animations

---

## License

MIT License — free to use, fork, and build upon.

---

## Built By

Developed for the Microsoft - Agents League Hackathon — Creative Apps Track.  
AI development assistant: GitHub Copilot.  
Runtime AI: Claude (Anthropic).  
IQ Layer: Work IQ (simulated).
