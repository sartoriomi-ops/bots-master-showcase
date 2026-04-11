# Architecture — bots-master

## Why wiki-first beats stateless bots

Most chatbot systems are stateless — every conversation starts from zero. The user (or an automation) has to re-explain context every time. This works for one-off questions but falls apart for ongoing workflows like content creation or job searching, where decisions build on each other over weeks.

The wiki-first approach solves this. Every bot reads from a shared, curated knowledge base before generating anything. When a bot discovers something useful, it writes it back to the wiki. Over time, the system gets smarter without any retraining — it just has better data to draw from.

## Data flow

```
External sources (web, job boards, social media)
        │
        ▼
┌──────────────┐
│   raw/       │  ← Content Scout, Job Bot deposit unprocessed data
└──────┬───────┘
       │ verification + curation
       ▼
┌──────────────┐
│   wiki/      │  ← Shared knowledge base (all bots read from here)
│              │     Contains: verified facts, brand voice, topic research,
│              │     skills profile, audience insights, past decisions
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   outputs/   │  ← Article Machine, Social Media, Job Bot write final
│              │     deliverables: posts, articles, applications
└──────────────┘
```

## Model routing policy

| Task type | Model | Reason |
|---|---|---|
| Content generation (articles, posts) | Claude Sonnet | Quality matters — these are public-facing |
| Research and scraping | Claude Haiku | High volume, low stakes |
| Job application drafts | Claude Sonnet | Needs nuance and personalization |
| Instagram reply drafts | Claude Haiku | Speed over polish, human reviews before posting |

## Orchestration

Make.com handles scheduling and routing between bots. Each bot is a Make scenario that calls the Claude API with a specific system prompt and reads/writes to the appropriate folder via Notion API (wiki) or direct file storage (raw/outputs).

Upstash Redis handles rate limiting and deduplication (e.g., don't re-scrape the same job post twice).

## Cost control

Hard cap: **$62/month** across all bots. Enforced via:
- Prompt caching for repeated system prompts
- Haiku-first for non-critical tasks
- Daily usage logging to a Notion dashboard
- Make.com scenario-level budget alerts
