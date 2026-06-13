# NEXUS — Technical Architecture

## Single-File Architecture

NEXUS is intentionally built as a **single HTML file** (`index.html`) with zero build steps, zero npm dependencies, and zero configuration. This was a deliberate choice for the hackathon:

- **Deploy anywhere instantly** — GitHub Pages, Netlify, any static host
- **Zero friction** — no `npm install`, no webpack, no compilation
- **Reviewable** — judges can read the entire codebase in one file
- **Demonstrates skill** — complex UI without framework scaffolding

## Page System

NEXUS implements a custom single-page application router:

```javascript
function goPage(p) {
  // Hide all pages
  document.querySelectorAll('.page').forEach(x => x.classList.remove('active'));
  // Show target page with CSS animation
  document.getElementById('page-' + p).classList.add('active');
  // Update bottom nav state
  document.querySelectorAll('.bnav-btn').forEach(x => x.classList.remove('active'));
  document.getElementById('bn-' + p)?.classList.add('active');
  // Trigger page-specific render
  if (p === 'memory') renderMemory();
  if (p === 'lb') renderLeaderboard();
  if (p === 'threats') renderThreats();
  window.scrollTo(0, 0);
}
```

CSS page transitions use `@keyframes pageIn` for a smooth entrance animation.

## Data Model

All threat data is stored in a static `THREATS` array:

```javascript
{
  id: 'ai',                    // unique key
  icon: '🤖',                  // emoji
  name: 'AI Singularity',      // display name
  color: '#8b5cf6',            // theme color
  risk: 88,                    // risk percentage (0-100)
  tag: 'EXTREME',              // badge text
  tagColor: '...',             // badge background
  tagText: '...',              // badge text color
  img: '...',                  // Unsplash URL
  casualties: '...',           // intelligence data
  riskIndex: '88%',            // formatted
  classification: 'Extreme',   // severity class
  sources: '...',              // data attribution
  desc: '...',                 // one-line description
  timeline: [                  // 5 events
    { y: '2025', e: '...', done: true },
    { y: '2027', e: '...', active: true },
    { y: '2029', e: '...', proj: true }   // (proj = projected)
  ],
  decision: {
    q: '...',                  // decision question
    opts: ['...', '...', '...', '...']  // 4 options, each containing "+N%" or "-N%"
  }
}
```

## Survival Delta Parsing

Decision impact is parsed directly from option text — no separate data structure needed:

```javascript
const match = allOpts[idx].match(/([+\-]\d+)%/);
const delta = match ? parseInt(match[1]) : 0;
```

This keeps the data self-documenting — the displayed text and the game logic are one and the same.

## Canvas Radar Chart

The global threat index radar chart is drawn with the HTML5 Canvas API:

```javascript
function drawRadar() {
  // 1. Draw 4 concentric polygon rings (grid)
  // 2. Draw spokes from center to each vertex
  // 3. Plot threat values as filled polygon
  // 4. Draw dots at each data point (colored per threat)
  // 5. Label each axis
}
```

## AI Integration

Claude API is called client-side on each decision:

```
POST https://api.anthropic.com/v1/messages
Model: claude-sonnet-4-6
Max tokens: 200

System context: NEXUS oracle persona
User message: Decision + threat context + survival change + Work IQ history
```

Fallback responses (4 variants) activate on any network/API error, ensuring the experience works without connectivity.

## State Management

```javascript
let state = {
  survival: 70,              // current civilization survival %
  decisions: 0,              // total decisions this session
  memory: [],                // persisted to localStorage
  scores: [],                // persisted to localStorage
  activeThreat: null         // currently loaded threat ID
};
```

State is in-memory for the session, with `memory` and `scores` arrays synced to `localStorage` on every decision.

## CSS Architecture

Custom properties (CSS variables) define the entire token system:

```css
:root {
  /* Backgrounds */
  --bg: #03050d;  --bg2: #070b18;  --bg3: #0c1220;
  /* Cards */
  --card: #0e1628;  --card2: #141e35;
  /* Borders */
  --border: #1a2740;  --border2: #243550;
  /* Text */
  --text: #dde6f0;  --text2: #7a9ab8;  --text3: #374f6a;
  /* Accents — one per threat + UI states */
  --blue: #3b82f6;  --red: #ef4444;  --amber: #f59e0b;
  --green: #10b981;  --purple: #8b5cf6;  --cyan: #06b6d4;
  /* Fonts */
  --orb: 'Orbitron', monospace;
  --grotesk: 'Space Grotesk', sans-serif;
  --mono: 'JetBrains Mono', monospace;
}
```

The `body::after` scanline overlay (CSS `repeating-linear-gradient`) adds CRT texture without performance impact.
