# Bots Master Showcase

A wiki-first multi-bot system built on Claude API, Make.com, Upstash, Notion, and Telegram.

## Status: Week 0 — Scoping Phase

No bots are built yet. All 8 are in architectural scoping. This repo documents the journey from zero to a production bot fleet.

## Planned Bots (8 total)

| Bot | Purpose | Status |
|-----|---------|--------|
| Job Bot | Poll listings and surface relevant matches via Telegram | Week 1 build priority |
| Content Scout | Surface trending topics for content brands | Scoping |
| Interviewer | Mock interview practice with feedback | Scoping |
| Article Machine | Draft long-form content from outlines | Scoping |
| Social Media | Schedule and format posts across platforms | Scoping |
| IG Replies | Auto-respond to Instagram comments | Scoping |
| Gmail Sorter | Classify and prioritize inbox | Scoping |
| Finance Analyzer | Track expenses and flag anomalies | Scoping |

## Stack

- Claude API (Sonnet for speed, Opus for complex tasks)
- Make.com (sole automation platform)
- Upstash (Redis for state and rate limiting)
- Notion (triple-logging across 3 databases)
- Telegram (delivery and alerts)

## Architecture

Each bot follows a wiki-first approach: full specification documented before any code is written. See the /wiki folder for bot specs as they are completed.

## Author

Michelle Sartorio — [michellesartorio.com](https://michellesartorio.com)
