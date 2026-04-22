# Invoice Agent — Project Intelligence

> This file is read automatically at the start of every session.
> Add context here as the project grows — patterns, decisions, research, domain knowledge.
> When asked to "make an agent", use everything in this file as the agent's training context.

---

## Skills — Auto-load every session

Always invoke these skills at the start of any design or UI task:

| Skill | Purpose |
|---|---|
| `/frontend-design` | Polished, intentional code — no generic AI aesthetics |
| `/ui-ux-pro-max` | UX heuristics, animation patterns, interaction states |
| `/impeccable` | Anti-patterns, easing, spacing precision, AI slop test |
| `/web-design-guidelines` | Vercel 100+ rules: accessibility, focus, forms, animation |
| `/fiori` | SAP Fiori + UI5 component selection |
| `/fiori-design` | Horizon tokens, spacing, typography, accessibility |

These work **within** SAP Horizon Morning — they don't override it.

---

## What This Project Is

A clickable prototype of an SAP Ariba invoice processing experience with a Joule AI assistant panel.
Built for demo and presentation to SAP stakeholders.

**Goal:** Show how an AI-powered invoice agent (Joule) can guide a user through invoice processing —
from search → typeahead → Joule conversation → invoice selection → approval submission.

---

## People & Context

- **Owner:** Product designer at SAP, no coding background
- **Audience:** SAP internal stakeholders (on VPN)
- **Purpose:** Design prototype / vision demo — not a production app

---

## Current State of the App

**Format:** Plain HTML/CSS/JS — single file, opens by double-clicking
**File:** `invoice-agent.html`
**Live URL (SAP):** `https://pages.github.tools.sap/I515936/invoice-agent/invoice-agent.html`
**Live URL (public):** `https://wenyang33.github.io/invoice-agent/invoice-agent.html`
**Repo (SAP):** `https://github.tools.sap/I515936/invoice-agent`
**Repo (public):** `https://github.com/wenyang33/invoice-agent`

### 3 States / Flow

| State | Trigger | What shows |
|---|---|---|
| Landing | Page load | SAL home page — shell bar, side nav, blue gradient search, dashboard widgets |
| Typeahead | Click search input | White rounded card dropdown with suggestions + catalog products |
| Joule overlay | Click first suggestion | Joule panel slides in bottom-right (448px wide, purple gradient header) |

---

## Design System

**Theme:** SAP Horizon Morning — always, no exceptions
**Font:** `'72', 'Segoe UI', Arial, sans-serif`
**Spacing base:** 8px

### Key Tokens
| Token | Value |
|---|---|
| Primary blue | `#0070F2` |
| Shell background | `#FFFFFF` |
| Page background | `#F7F7F7` |
| Border | `#EDEDED` |
| Text primary | `#131e29` |
| Text secondary | `#556b82` |
| Link / highlight | `#0064d9` |
| Selection bg | `#ebf8ff` |
| Success | `#107E3E` |
| Warning | `#E8710A` |
| Error | `#E72B42` |

### Joule Panel Tokens
| Element | Value |
|---|---|
| Header gradient | `linear-gradient(180deg, #5d36ff → #6431fa)` |
| User bubble | `#eff1f2` — border-radius `8px 8px 0 8px` |
| AI bubble | `#eae5ff` — border-radius `8px 8px 8px 0` |
| Input border (focus) | `#5d36ff` |
| Send button | `#5d36ff` |
| Panel width | `448px` |
| Header height | `56px` |

---

## UI Components Built

| Component | Location in file | Notes |
|---|---|---|
| Shell bar | `.shell-bar` | SAP logo, search, Joule btn, notifications, avatar |
| Side navigation | `.side-nav` | 256px wide, Home active, Invoice expanded with children |
| Blue gradient search zone | Inside `.search-bar-wrap` | `#0057d2` gradient bg, anvil SVG shapes, white pill input |
| Typeahead dropdown | `.typeahead-dropdown` | `border-radius: 17px`, shadow from Figma, 3 rows + Catalog section |
| Joule panel | `.joule-popover` | Fixed bottom-right, 448px, purple header, chat bubbles, input |
| Dashboard widgets | `.content-grid` | Announcement, Documents table, Invoice Categories, Insights charts |
| Right column | `.col-right` | To-dos, Quick Links |

---

## Typeahead Exact Specs (from Figma frame 4-80340)

- Container: white card, `border-radius: 17px`
- Shadow: `0px 4px 16px rgba(34,53,72,0.16), 0px 0px 2px rgba(34,53,72,0.12)`
- Row 1 "Hiring 25 engineers...": background `#ebf8ff`, full opacity
- Rows 2–3: `opacity: 0.6`
- "Catalog" header: `72:Bold`, `#556b82`, 12px
- Product rows: 48×48px image, `border-radius: 12px`, also `opacity: 0.6`
- MacBook Pro: Apple · TX71002-422CAL · **2,700.00 USD / item**
- ThinkPad X1 Carbon: Lenovo · 21HM004GUS · **1,899.00 USD / item**

---

## Figma Source Files

| Frame | Node ID | Description |
|---|---|---|
| Landing page | `3-76515` | Full SAL home — shell, nav, search zone, widgets |
| Typeahead | `4-80340` | Search suggestions + catalog product rows |
| Joule overlay | `5-81727` | Joule chat panel — bottom-right overlay |
| File key | `ObFAb4jjfT6ZTpXzYUc8BV` | Main design file |

**Rule — 1:1, NO EXCEPTIONS:** Before every single `use_figma` write call, screenshot the **exact reference node** you are building against. One screenshot = one write. The flag resets after every write — no batching. Taking a screenshot of a different node does not count. Pattern: screenshot → write → screenshot → write.

---

## Joule Loading Sequence — MANDATORY PATTERN

Every time Joule is about to show a card or the explainability loader, the sequence MUST be:

1. **Dot loader first** (always) — 3 purple dots, bare on white background, no bubble container
   - CSS: `.joule-dots-bubble` with `.jdot .jdot-1/2/3`
   - Figma: `lwF70Sz1KC7VbK1FmpIP5x` node `86692-15470`
2. **Skeleton card** (before cards/results) — shimmer placeholder cards
   - CSS: `.joule-skeleton-card` with `.skel-thumb`, `.skel-row`, `.skel-badge`
   - Figma: `lwF70Sz1KC7VbK1FmpIP5x` node `81047-67509`
3. **Explainability loader** (if showing process steps) — named steps with progress bar
4. **Response / card** — actual content

Simple text responses: dots only → then text bubble (no skeleton needed).
Cards / product results: dots → skeleton → loader (if applicable) → card.

---

## Tech Rules

- **Always plain HTML** for this prototype — no React, no build step, no Node
- File must open by double-clicking in a browser
- Never use Tailwind, never use React for this project
- Always check Figma before writing or updating any UI element
- Always confirm with user before `git commit` or `git push`
- Always verify `invoice-agent.html` is in the `/invoice-agent/` project folder

---

## Git / Deploy Rules

- Repo (SAP): `github.tools.sap/I515936/invoice-agent`
- Repo (public): `github.com/wenyang33/invoice-agent`
- GitHub Pages URL (SAP): `https://pages.github.tools.sap/I515936/invoice-agent/invoice-agent.html`
- GitHub Pages URL (public): `https://wenyang33.github.io/invoice-agent/invoice-agent.html`
- Always show local file path AND GitHub Pages URL after any deploy
- Always confirm commit message with user before pushing
- Source HTML must always be committed — never commit without source

---

## Procurement Domain Context

*(Add here as you train me — supplier rules, contract types, approval flows, SAP Ariba terminology, research data, agent behaviour patterns etc.)*

---

## Joule / Agent Behaviour Patterns

*(Add here — how Joule should respond, what procurement tasks it handles, conversation patterns, what cards/tables it generates, tool calls it makes etc.)*

---

## Research & Reference Data

*(Add here — user research findings, competitor analysis, SAP product strategy context, stakeholder feedback etc.)*

---

## Dev Handoff — Joule Panel Component Mapping

> The SAL page (shell, nav, dashboard) is already built — this covers the Joule panel only.
> Library: Joule Web UI Kit (`lwF70Sz1KC7VbK1FmpIP5x`)
> Figma reference frames (04–10): [CC_Write](https://www.figma.com/design/uwrn21ALPsGFF8WoCcGXpm/CC_Write)

### Joule Panel Structure

| What it does | Component | Notes |
|---|---|---|
| Outer panel shell | `JouleShell` | Purple gradient header, fullscreen or overlay mode |
| User message bubble | `JouleUserMessage` | Right-aligned, light purple bg `#EAE5FF` |
| AI response bubble | `JouleAssistantMessage` | Left-aligned, grey bg `#EFF1F2` |
| 3-dot typing indicator | `JouleLoadingMessage` | Dots only — always shown first, before any response |
| Skeleton card loader | `JouleSkeletonCard` | Shown after dots, before real cards load |
| Explainability loader | `JouleDeepResearchCard` | Streaming steps with progress bar — see frame 06 |
| Product result card | `JouleObjectCard` / `JouleListCard` | See frame 08 — DEWALT preferred, contract badges |
| Quick reply chips | `JouleQuickReply` | e.g. "Proceed with DEWALT", "Compare all options" |
| Input bar | `JouleInputBar` | Bottom, purple border + send button |
| Disclaimer | `JouleDisclaimer` | "Joule uses AI, verify results." |

### Loading Sequence — MANDATORY

Every Joule response must follow this exact order (see frames 04→07):

```
dots (JouleLoadingMessage)
  → skeleton (JouleSkeletonCard)        ← only if showing cards
    → explainability (JouleDeepResearchCard)  ← only if showing reasoning steps
      → result (JouleObjectCard / JouleAssistantMessage)
```

Simple text reply: dots → text bubble only (no skeleton).

### Conversation State (suggestion)

```js
// Each turn in the conversation array:
{ role: 'user' | 'joule', type: 'text' | 'cards' | 'cart', content, loading: 'dots' | 'skeleton' | 'loader' | null }
```

---

## Decisions Log

| Date | Decision | Reason |
|---|---|---|
| 2026-04 | Plain HTML not React | Designer needs double-click file, no dev setup |
| 2026-04 | Figma MCP before all UI code | Previous code looked wrong when written from memory |
| 2026-04 | GitHub Pages for sharing | Public GitHub Pages for easy sharing |
| 2026-04 | 448px Joule panel width | Matched exactly from Figma frame 5-81727 |
