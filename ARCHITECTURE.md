<div align="center">

# 🏗️ Architecture

**How the bots-master system works under the hood.**

</div>

---

## 💡 Why wiki-first beats stateless bots

Most chatbot systems are stateless. Every conversation starts from zero. The user has to re-explain the context every time.

That works for one-off questions. It falls apart for ongoing workflows like content creation or job searching, where decisions build on each other over weeks.

The wiki-first approach solves this:

1. Every bot **reads** from a shared, curated knowledge base before generating anything.
2. When a bot discovers something useful, it **writes** it back to the wiki.
3. Over time, the system gets smarter without changing any prompts. It just has better data to draw from.

---

## 🔄 Data flow

```
External sources (web, job boards, email, social media)
         │
         ▼
┌────────────────┐
│   raw/         │  ← Bots deposit unprocessed data here
└───────┬────────┘
        │  verification + curation
        ▼
┌────────────────┐
│   wiki/        │  ← Shared knowledge base (all bots read from here)
│                │     Verified facts, brand voice, topic research,
│                │     skills profile, audience insights, past decisions
└───────┬────────┘
        │
        ▼
┌────────────────┐
│   outputs/     │  ← Final deliverables:
│                │     Posts, articles, applications, reports
└────────────────┘
```

> Every output goes through human review. No bot output goes public without approval.

---

## 🧠 Model routing

Each bot uses the right-sized model for its task.

| Task type | Model tier | Examples |
|---|---|---|
| Content generation, nuanced writing | Capable model | Article Machine, Social Media |
| Classification, scraping, sorting | Fast lightweight model | Gmail Sorter, Content Scout |

This keeps quality high on creative work and costs low on repetitive tasks.

---

## ⚙️ Orchestration

```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  Cron /  │────▶│ Make.com │────▶│ Claude   │────▶│ Telegram │
│ Trigger  │     │ Scenario │     │ API      │     │ Output   │
└──────────┘     └────┬─────┘     └──────────┘     └──────────┘
                      │
                      ▼
               ┌──────────┐
               │ Notion   │
               │ Log      │
               └──────────┘
```

Each bot runs on its own schedule inside Make.com. Each one calls the Claude API with a specific system prompt and reads/writes to the appropriate wiki folder. Deduplication prevents bots from reprocessing the same input twice.

---

## 💰 Cost control

The system runs under a fixed monthly budget. Four mechanisms enforce it:

| Mechanism | What it does |
|---|---|
| **Prompt caching** | Reuses wiki context across calls to reduce token usage |
| **Model routing** | Routes simple tasks to cheaper models |
| **Usage logging** | Every API call is logged with token count and cost |
| **Budget alerts** | Make.com triggers a warning when spend approaches the cap |

---

<div align="center">

*This is a living document. It updates as bots move from scoped to shipped.*

</div>
