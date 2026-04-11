# Architecture — bots-master

## Why wiki-first beats stateless bots

Most chatbot systems are stateless — every conversation starts from zero. The user (or an automation) has to re-explain context every time. This works for one-off questions but falls apart for ongoing workflows like content creation or job searching, where decisions build on each other over weeks.

The wiki-first approach solves this. Every bot reads from a shared, curated knowledge base before generating anything. When a bot discovers something useful, it writes it back to the wiki. Over time, the system gets smarter without any retraining — it just has better data to draw from.

## Data flow

```
External sources (web, job boards, email, social media)
        │
        ▼
┌──────────────┐
│   raw/       │  ← Bots deposit unprocessed data here
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
│   outputs/   │  ← Bots write final deliverables:
│              │     posts, articles, applications, reports
└──────────────┘
```

## Model routing

Each bot uses the right-sized model for its task. Content generation and tasks requiring nuance use a more capable model. High-volume classification tasks like email sorting and initial scraping use a faster, lighter model. Every call is reviewed before shipping — no bot output goes public without human approval.

## Orchestration

An automation platform handles scheduling and routing between bots. Each bot runs on its own schedule, calls the Claude API with a specific system prompt, and reads/writes to the appropriate wiki folder. Deduplication prevents bots from reprocessing the same input twice.

## Cost control

The system runs under a strict monthly budget enforced through prompt caching, model routing, usage logging, and automation-level budget alerts.
