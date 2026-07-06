# Multi-Agent Marketing Crew

> A fully autonomous AI marketing team built with [CrewAI](https://www.crewai.com/) — from product brief to ready-to-publish marketing assets in a single run.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![CrewAI](https://img.shields.io/badge/CrewAI-Multi--Agent-blueviolet)
![LLM](https://img.shields.io/badge/LLM-GPT--4o--mini-green?logo=openai)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## Overview

This project simulates a real marketing team using four specialized AI agents that collaborate sequentially to produce a complete weekly marketing workflow for any product. You provide a product name, target audience, and budget — the crew handles everything else.

Built as part of an end-to-end agentic AI exploration using CrewAI, this project demonstrates how multi-agent systems can replace hours of manual marketing work with a single command.

---

## Agent Pipeline

```text
┌─────────────────────────────────────────────────────────────────┐
│                     Input: Product Brief                        │
│         (product name, audience, budget, current date)          │
└──────────────────────────┬──────────────────────────────────────┘
                           │
               ┌───────────▼───────────┐
               │   Head of Marketing   │
               │  Market Research      │
               │  Marketing Strategy   │
               └───────────┬───────────┘
                           │
          ┌────────────────▼────────────────┐
          │   Content Creator (Social)      │
          │  Content Calendar               │
          │  Social Post Drafts             │
          │  Instagram Reel Scripts         │
          └────────────────┬────────────────┘
                           │
            ┌──────────────▼──────────────┐
            │   Content Writer (Blogs)    │
            │  Blog Research              │
            │  Blog Drafts                │
            └──────────────┬──────────────┘
                           │
             ┌─────────────▼─────────────┐
             │      SEO Specialist       │
             │   SEO-Optimized Blogs     │
             └─────────────┬─────────────┘
                           │
┌──────────────────────────▼──────────────────────────────────────┐
│                     Output: Marketing Assets                    │
│  strategy · calendar · posts · reel scripts · SEO blogs         │
└─────────────────────────────────────────────────────────────────┘
```

---

## Key Features

- **Autonomous end-to-end workflow** — runs market research, strategy, content, and SEO in one pipeline with no manual steps
- **4 specialized AI agents**, each with distinct roles, goals, and tool access
- **Real-time web research** via Serper search + website scraping tools
- **Structured file output** — all assets saved as markdown files, ready for review
- **Fully configurable** — swap product, audience, budget, or LLM in minutes
- **Sequential multi-agent planning** with CrewAI's built-in planning LLM layer

---

## Agent Roles

| Agent | Responsibility | Key Tools |
|---|---|---|
| Head of Marketing | Market research, competitor analysis, strategy planning | Serper, ScrapeWebsite, FileWriter |
| Content Creator (Social) | Content calendar, social posts, reel scripts | Serper, ScrapeWebsite, FileWriter |
| Content Writer (Blogs) | Blog research, outline, draft writing | Serper, ScrapeWebsite, FileWriter |
| SEO Specialist | Keyword optimization, meta tags, internal links | Serper, ScrapeWebsite, FileWriter |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Agent Framework | [CrewAI](https://github.com/crewAIInc/crewAI) |
| LLM | OpenAI GPT-4o-mini |
| Search Tool | Serper Dev API |
| Web Scraping | CrewAI ScrapeWebsiteTool |
| Data Validation | Pydantic v2 |
| Config | YAML (agents + tasks) |
| Language | Python 3.10+ |

---

## Project Structure

```text
marketing-crew/
├── crew.py                  # Agent + task definitions and crew orchestration
├── requirements.txt
├── .env.example
├── config/
│   ├── agents.yaml          # Agent roles, goals, backstories
│   └── tasks.yaml           # Task descriptions and expected outputs
└── resources/
    └── drafts/
        ├── marketing_strategy.md
        ├── content_calendar.md
        ├── posts/            # Social + email drafts
        ├── reels/            # Instagram reel scripts
        └── blogs/            # SEO-optimized blog drafts
```

---

## Quick Start

### 1. Clone and install

```bash
git clone https://github.com/ghanashyam9348/multi-agent-marketing-crew.git
cd multi-agent-marketing-crew
pip install -r requirements.txt
```

### 2. Set up environment

Copy `.env.example` to `.env` and fill in your keys:

```env
OPENAI_API_KEY=your_openai_api_key
SERPER_API_KEY=your_serper_api_key
```

### 3. Run

```bash
python crew.py
```

### 4. Check generated outputs

```text
resources/drafts/marketing_strategy.md   ← full marketing plan
resources/drafts/content_calendar.md     ← week-by-week schedule
resources/drafts/posts/                  ← LinkedIn, Twitter, Instagram, email
resources/drafts/reels/                  ← Instagram reel scripts
resources/drafts/blogs/                  ← SEO-optimized blog drafts
```

---

## Customize for Your Product

Edit the `inputs` dict in `crew.py`:

```python
inputs = {
    "product_name": "Your Product Name",
    "target_audience": "Your Target Audience",
    "product_description": "What your product does",
    "budget": "Your marketing budget",
    "current_date": datetime.now().strftime("%Y-%m-%d"),
}
```

The default demo runs for **AI Powered Excel Automation Tool** targeting SMEs with a Rs. 50,000 budget.

---

## Requirements

- Python 3.10+
- `OPENAI_API_KEY` — [OpenAI Platform](https://platform.openai.com/)
- `SERPER_API_KEY` — [Serper.dev](https://serper.dev/) (free tier available)

---

## Notes

- Rate limits are managed via `max_rpm=3` and per-agent `max_iter` settings to stay within API quotas.
- The `planning=True` flag enables CrewAI's built-in pre-execution plan generation using the same LLM.
- All tasks use `Process.sequential` — outputs chain from one agent to the next.