# Marketing Crew (CrewAI Multi-Agent Marketing Automation)

This project is a CrewAI-based multi-agent system that generates a complete weekly marketing workflow for a product, from market research to content planning and SEO-optimized drafts.

The crew includes specialized agents for strategy, social content, blog writing, and SEO. It uses web research and file tools to produce actionable outputs in markdown/text files.

## What This Project Does

- Runs end-to-end market and competitor research
- Builds a weekly marketing strategy aligned to product and audience
- Creates a content calendar
- Drafts social posts and email campaign content
- Generates Instagram reel scripts
- Researches and drafts blog content
- Applies SEO optimization guidance

## Agent Roles

- Head of Marketing: Owns research, strategy, and high-level planning
- Content Creator (Social): Creates content calendar, posts, and reel scripts
- Content Writer (Blogs): Researches and drafts blog content
- SEO Specialist: Optimizes content for search visibility

## Project Structure

```text
marketing-crew/
├── crew.py
├── config/
│   ├── agents.yaml
│   └── tasks.yaml
├── resources/
│   ├── drafts/
│   │   ├── posts/
│   │   └── reels/
│   └── saved_drafts/
└── README.md
```

## Requirements

- Python 3.10+
- API keys:
	- `OPENAI_API_KEY`
	- `SERPER_API_KEY` (for search tool)

## Installation

```bash
pip install crewai crewai-tools python-dotenv pydantic
```

## Environment Setup

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_api_key
SERPER_API_KEY=your_serper_api_key
```

## How to Run

```bash
python crew.py
```

## Default Input

The sample run in `crew.py` uses:

- Product: AI Powered Excel Automation Tool
- Audience: SMEs
- Budget: Rs. 50,000

You can edit the `inputs` dictionary in `crew.py` to target your own product and audience.

## Output Files

Generated outputs are saved under `resources/drafts/` and related folders.

Examples include:

- `resources/drafts/marketing_strategy.md`
- `resources/drafts/content_calendar.md`
- `resources/drafts/posts/`
- `resources/drafts/reels/`

## Notes

- The current LLM configuration in `crew.py` uses `openai/gpt-4o-mini`.
- Rate-limits are controlled with `max_rpm` and task `max_iter` settings.
- Some task expectations reference `resources/drafts/blogs/`; make sure this folder exists before production runs.


## Short Demo

### 1) Set up environment

```bash
pip install -r requirements.txt
```

Create a `.env` file:

```env
OPENAI_API_KEY=your_openai_api_key
SERPER_API_KEY=your_serper_api_key
```

### 2) Run the crew

```bash
python crew.py
```

### 3) Check generated outputs

After execution, review generated files in:

- `resources/drafts/marketing_strategy.md`
- `resources/drafts/content_calendar.md`
- `resources/drafts/posts/`
- `resources/drafts/reels/`

### 4) Customize for your use case

Edit the `inputs` dictionary in `crew.py` to change product, audience, budget, and campaign context.