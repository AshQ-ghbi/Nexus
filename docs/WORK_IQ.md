# Work IQ Integration — NEXUS

## Overview

NEXUS integrates a **Work IQ–inspired personal memory layer** as its core intelligence feature. This document describes the implementation in detail.

## What is Work IQ?

Work IQ is a Microsoft 365 Copilot intelligence layer that builds deep context from a user's work patterns — emails, meetings, documents, and relationships — to deliver personalized, grounded AI responses.

## How NEXUS Simulates Work IQ

### Storage Layer

```javascript
// Decision stored to localStorage on every choice
const entry = {
  threat: tid,           // threat ID
  threatName: t.name,    // human-readable name
  icon: t.icon,          // emoji icon
  choice: choice,        // full decision text
  delta: delta,          // survival impact (+/- %)
  survival: state.survival, // running total
  date: new Date().toLocaleDateString()
};

state.memory.unshift(entry);
localStorage.setItem('nexus_mem', JSON.stringify(state.memory));
```

### Context Injection

```javascript
// Last 3 decisions injected into every Claude API prompt
const prev = state.memory.slice(1, 4)
  .map(m => `${m.threatName}: "${m.choice.substring(0, 50)}" (${m.delta > 0 ? '+' : ''}${m.delta}%)`)
  .join(' | ');

const prompt = `
  You are NEXUS, a civilization collapse AI oracle.
  The user chose: "${choice}" for threat: ${t.name}.
  Survival changed by ${delta}%. Current: ${state.survival}%.
  Their decision history: ${prev || 'First decision'}.
  
  Write 3 sentences analyzing:
  1. Immediate consequence of this choice
  2. Long-term civilizational impact
  3. What behavioral archetype this reveals
`;
```

### Pattern Detection (UI Layer)

The memory page surfaces behavioral patterns:
- **Total decisions** across all sessions
- **Positive outcome ratio** (decisions that increased survival)
- **Per-threat history** with full decision text and survival impact

### Work IQ Hint System

Before every simulation, NEXUS checks memory for prior decisions on that threat:

```javascript
const mem = state.memory.filter(m => m.threat === id);
const memHint = mem.length
  ? `Work IQ Memory · You've faced this threat ${mem.length}× before. Last: "${mem[0].choice}"`
  : `Work IQ: No prior decisions on this threat. Your choice will be remembered.`;
```

## Comparison: Work IQ vs NEXUS Implementation

| Dimension | Microsoft Work IQ | NEXUS Work IQ Layer |
|---|---|---|
| **Data source** | Emails, meetings, documents | Crisis decisions, simulation outcomes |
| **Context window** | Recent work history | Last 3–5 decisions |
| **Personalization** | Adapts Copilot responses | Adapts AI threat analysis |
| **Storage** | Microsoft Graph / cloud | localStorage (client-side) |
| **Pattern surfacing** | Relationship insights, topics | Behavioral archetype detection |
| **Persistence** | Cross-device, cloud sync | Single-device, session-persistent |

## Behavioral Archetypes

Based on decision patterns, NEXUS identifies 4 archetypes:

| Archetype | Pattern | Example |
|---|---|---|
| **Pragmatist** | Accepts trade-offs for immediate gain | Chooses +12% with collateral damage |
| **Idealist** | Favors institutional and multilateral solutions | Consistently picks UN-based options |
| **Technocrat** | Prioritizes technological interventions | Always selects AI/tech-based responses |
| **Militarist** | Prefers decisive, forceful responses | Chooses containment via military options |

The Claude prompt explicitly asks for archetype identification in the 3rd analysis sentence.
