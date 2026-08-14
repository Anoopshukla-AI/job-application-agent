# Job Application Agent

A production-grade n8n AI agent that automates job discovery, fit-scoring, and outreach drafting for AI Automation Engineer / n8n Developer roles — built to solve my own job search and double as a portfolio piece demonstrating production AI-agent design.

## What It Does

1. Polls LinkedIn, Naukri, and Indeed every 12 hours for fresh postings
2. Deduplicates using a SHA-256 hash of `company|title|apply_url` (idempotent — safe to re-run)
3. Scores each posting against my resume/profile via GPT-4o using a versioned rubric stored in Notion (`Scoring Config` page)
4. For scores >= 70: drafts a personalized 4-line outreach message and logs everything to Notion
5. Sends a Telegram alert only for high-match roles — no spam, no auto-apply
6. Every run writes structured logs (trace_id, node, status, latency, tokens used) to an Execution Log; any failure routes to a centralized Error Handler workflow with its own Notion log + Telegram alert

## Why This Design

Most "job search bot" tutorials skip production concerns entirely. This version is built against a 2026 AI-agent production-readiness checklist:

- **Idempotency**: SHA-256 dedup hash prevents duplicate processing/alerts on re-runs
- **Retry strategy**: exponential backoff (3 tries, 2s/4s/8s) on every HTTP node
- **Centralized error handling**: a dedicated Error Handler workflow (see `workflows/error-handler-workflow.json`) catches failures from the main workflow via n8n's built-in error workflow setting
- **Observability**: every run logs trace_id, node, latency, and token usage to a Notion Execution Log
- **Cost governance**: token usage tracked per run to support a monthly budget cap
- **No blind automation**: outreach messages are drafted, never auto-sent — a human always reviews before applying
- **Self-improving loop**: a weekly recalibration pass reviews real outcomes (Applied → Interview vs Rejected/Ghosted) and updates the scoring rubric in Notion

## Files

- `workflows/main-workflow.json` — importable n8n workflow (main pipeline)
- `workflows/error-handler-workflow.json` — importable n8n error-handling workflow
- `docs/scoring-prompt.md` — the AI scoring rubric and prompt template

## Setup

1. Import both JSON files into your n8n instance (Workflows → Import from File)
2. Replace all `REPLACE_WITH_*` placeholders with your actual Notion database IDs and Telegram chat ID
3. In the main workflow's Settings, set "Error Workflow" to the imported Error Handler workflow
4. Add your job-source API credentials (LinkedIn/Naukri/Indeed)
5. Activate the workflow

## Stack

n8n · GPT-4o · Notion API · Telegram Bot API

---
Built by [Anoop Shukla](https://github.com/Anoopshukla-AI) — AI Automation Engineer specializing in agentic workflow orchestration.
