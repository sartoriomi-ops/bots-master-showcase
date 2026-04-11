# bots-master (architecture preview)

**Wiki-first 6-bot system built on Claude Managed Agents.**

---

## What it is

A coordinated system of six specialized bots that handle content research, writing, social media, and job search automation. Each bot reads from and writes to a shared knowledge base (the "wiki"), so context accumulates over time instead of being lost between sessions.

## The bots

| Bot | Role |
|---|---|
| **Content Scout** | Finds trending topics, news, and content angles across the web |
| **Interviewer** | Conducts structured research interviews on a topic and logs insights to the wiki |
| **Article Machine** | Writes long-form articles from wiki research — no hallucination, sources only |
| **Social Media** | Generates platform-specific posts (LinkedIn, Instagram, X) from wiki content |
| **Instagram Replies** | Monitors and drafts contextual replies using brand voice |
| **Job Bot** | Scans job boards, matches against skills profile, drafts tailored applications |

## Architecture

The system follows a **Karpathy three-folder structure**:

```
bots-master/
├── raw/        ← unprocessed inputs (scraped articles, job posts, notes)
├── wiki/       ← curated knowledge base (verified facts, insights, decisions)
└── outputs/    ← final deliverables (posts, articles, applications)
```

Every bot reads from `wiki/` and writes outputs to `outputs/`. Raw data enters through `raw/` and gets promoted to `wiki/` only after verification. This prevents hallucination drift — bots never generate from thin air, only from curated wiki entries.

See [ARCHITECTURE.md](./ARCHITECTURE.md) for the full data flow and model policy.

## Key decisions

- **Shared voice document:** All content bots reference a single voice/tone file so brand consistency is automatic.
- **Prompt caching:** Frequently used system prompts are cached to reduce API costs.
- **Sonnet-first model policy:** Default to Claude Sonnet for quality. Haiku only for high-volume, low-stakes tasks (like initial web scraping).
- **Cost cap:** $62/month hard limit across all six bots.

## Stack

`Claude API` · `Make.com` · `Upstash Redis` · `Notion API` · `Telegram Bot API`

## Status

🔧 **In active build** — Content Scout and Article Machine functional. Remaining bots in development.
