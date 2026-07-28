# Creator Discovery Agent

An AI-powered pipeline that automatically discovers YouTube Shorts creators for a brand or product.

Instead of manually searching through YouTube, the system generates search strategies with an LLM, discovers creators, enriches them with channel analytics, filters unsuitable candidates, and produces a structured creator database ready for outreach.

---

## Features

- AI-generated search keywords based on the product
- Multi-stage LangGraph workflow
- Automatic YouTube Shorts creator discovery
- Channel enrichment using YouTube Data API
- Budget-aware creator filtering
- Engagement and audience quality filtering
- Duplicate removal across multiple searches
- Structured JSON export for CRM or outreach

---

## Workflow

```
Brand Description
       │
       ▼
Keyword Generation (LLM)
       │
       ▼
Search YouTube Shorts
       │
       ▼
Collect Unique Channels
       │
       ▼
Fetch Channel Analytics
       │
       ▼
Build Creator Profiles
       │
       ▼
Budget Filtering
       │
       ▼
Quality Filtering
       │
       ▼
Export Results
```

---

## Architecture

The pipeline is implemented as a LangGraph workflow.

### 1. Intake

Accepts:

- Product description
- Budget tier
- Target location

Example:

```python
{
    "product_description": "AI fitness app",
    "budget_tier": "mid",
    "location": "United States"
}
```

---

### 2. AI Keyword Generation

Uses an LLM (OpenRouter) to generate realistic YouTube search keywords.

Instead of inventing keywords, the model generates phrases creators actually use in titles and descriptions.

Example:

```
fitness
home workout
gym motivation
desk workout
healthy habits
```

---

### 3. Creator Discovery

Each keyword is searched on YouTube Shorts.

The system:

- collects videos
- extracts unique channel IDs
- avoids duplicate creators

---

### 4. Creator Enrichment

Each creator is enriched with channel metadata including:

- subscriber count
- total views
- engagement
- country
- bio
- recent Shorts
- matched keywords

---

### 5. Budget Filtering

Creators are filtered based on campaign budget before moving further.

This removes creators outside the target pricing range.

---

### 6. Quality Filtering

Additional mathematical filters remove low-quality creators.

Examples include:

- minimum subscribers
- minimum engagement
- minimum average views
- maximum channel size

---

### 7. Export

Results are exported as structured JSON containing:

- creator profile
- analytics
- matched keywords
- recent Shorts
- run metadata

This output can directly feed into outreach tools or CRMs.

---

## Tech Stack

- Python
- LangGraph
- OpenRouter
- YouTube Data API
- OpenAI SDK
- dotenv

---

## Project Structure

```
nodes/
    intake.py
    keyword_gen.py
    search.py
    enrich.py
    filter_and_log.py
    rank.py

graph/
tools/
```

Each node performs one stage of the pipeline, making it easy to extend or replace.

---

## Why AI?

Traditional creator discovery relies on manually searching YouTube.

This system automates:

- search strategy generation
- creator discovery
- profile enrichment
- filtering
- shortlist creation

reducing hours of manual work into a single automated workflow.

---

## Future Improvements

- Multi-platform creator discovery (TikTok, Instagram, X)
- Semantic creator matching using embeddings
- Audience overlap analysis
- Brand safety scoring
- Outreach automation
- CRM integrations
- Campaign performance feedback loop

---

## Example Use Cases

- Influencer marketing agencies
- Brand partnerships
- Affiliate recruitment
- UGC creator discovery
- Product launch campaigns
- Creator prospecting
