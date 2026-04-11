# bots-master

**Wiki-first multi-bot system built on Claude Managed Agents.**

> Status: Early development. Architecture defined, first bots in progress.

---

## What it is

A coordinated system of specialized bots that handle content research, writing, social media, inbox management, and job search automation. Each bot reads from and writes to a shared knowledge base (the "wiki"), so context accumulates over time instead of being lost between sessions.

## The bots

| # | Bot | Role |
|---|-----|------|
| 1 | **Content Scout** | Finds trending topics, news, content angles |
| 2 | **Interviewer** | Structured research interviews, logs insights to wiki |
| 3 | **Article Machine** | Writes long-form articles from wiki research |
| 4 | **Social Media** | Platform-specific posts (LinkedIn, Instagram, X) |
| 5 | **Instagram Replies** | Brand-voice replies on Instagram |
| 6 | **Job Bot** | Scans job boards, matches profile, drafts applications |
| 7 | **Gmail Sorter** | Classifies email, applies labels, feeds relevant data to wiki |
| 8 | **Finance Analyzer** | Reads transactions periodically, generates summaries |

## Architecture

Karpathy three-folder structure:
```
bots-master/
├── raw/      ← unprocessed inputs
├── wiki/     ← curated knowledge base
└── outputs/  ← final deliverables
```

Every bot reads from `wiki/` and writes outputs to `outputs/`. Raw data enters through `raw/` and is promoted to `wiki/` only after verification. This prevents hallucination drift.

## Design principles

- **Shared voice document** across all content bots for brand consistency
- **Prompt caching** on frequently used system prompts to reduce latency and cost
- **Model routing** — right-sized models per task instead of one-size-fits-all

---

*Last updated: 2026-04-12*
