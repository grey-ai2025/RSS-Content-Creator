---
description: Scrape RSS feeds for research then generate LinkedIn briefs
---

Run the full LinkedIn content pipeline:

## Stage 0: LinkedIn Benchmark

Use the `linkedin-analyzer` subagent to scrape top AI/tech influencer LinkedIn profiles and analyze their highest-performing recent posts.

The agent uses Firecrawl MCP tools to scrape influencer activity pages, identifies the top 10-15 posts by engagement, and extracts patterns (hook styles, formats, topics, structure). It saves a benchmark file to `content/benchmarks/`.

This stage runs first so downstream agents (SEO, drafting, ranking) can reference the benchmark data.

## Stage 1: SEO Keywords

Use the `seo-researcher` subagent to research trending AI/tech keywords for LinkedIn.

The agent uses Google Trends MCP tools directly to find currently trending topics, then supplements with web searches for LinkedIn-specific hashtag and engagement data. It saves a structured keywords file to `content/seo/`.

## Stage 2: Research

Once SEO keywords are ready, use the `news-researcher` subagent to fetch the latest news from these RSS feeds:

- https://technologyreview.com/topic/artificial-intelligence/feed
- https://wired.com/feed/tag/ai/latest/rss
- https://techcrunch.com/category/artificial-intelligence/feed
- https://theverge.com/rss/ai-artificial-intelligence/index.xml
- https://venturebeat.com/category/ai/feed
- https://arstechnica.com/ai/feed
- https://nytimes.com/svc/collections/v1/publish/www.nytimes.com/spotlight/artificial-intelligence/rss.xml
- https://fastcompany.com/section/artificial-intelligence/rss
- https://unite.ai/feed
- https://dailyai.com/feed
- https://artificialintelligence-news.com/feed
- https://aiweekly.co/issues.rss
- https://aihub.org/feed/?cat=-473
- https://datamachina.substack.com/feed
- https://sciencedaily.com/rss/computers_math/artificial_intelligence.xml

The agent should read the keywords file from `content/seo/` to guide story selection — prioritizing stories that align with trending topics. It must sort all feed items by publication date (newest first) so the most recent stories are always covered. After selecting candidates, the agent must apply same-day thematic deduplication — grouping stories by core theme and keeping only the strongest per theme to prevent overlapping posts. Save research summaries to `content/research/`.

## Stage 3: Brief Generation

Once research is complete, use the `draft-writer` subagent to generate structured briefs for the LinkedIn Growth Engine from any new research files that don't already have a matching brief.

The agent should read the keywords file from `content/seo/` and save briefs to `content/drafts/`. Before writing, the agent must check all existing briefs from the past 7 days for thematic overlap — skipping any research file whose core theme is already covered by an existing brief.

## Stage 4: Ranking

Once all briefs are written, use the `post-ranker` subagent to score every brief against the brief scoring rubric, rank them, and pick the winner.

The agent should write a ranking report to `content/drafts/_ranking.md` and update each brief's frontmatter status (`winner` for the top pick, `ranked` for the rest).

## Stage 5: Compilation

Once ranking is complete, use the `content-compiler` subagent to compile all of today's ranked briefs and their source research into a single review file.

The agent reads the ranking from `content/drafts/_ranking.md`, pairs each brief with its research file in rank order, and writes the compilation to `content/google doc/YYYY-MM-DD.md` for review in Google Docs.

## Stage 6: Report

After all stages are done, list what was created:

1. LinkedIn benchmark file in `content/benchmarks/`
2. SEO keywords file in `content/seo/`
3. New files in `content/research/`
4. New files in `content/drafts/`
5. The ranking results — show the full scoreboard and announce the winner
6. Compilation file in `content/google doc/`

Summarize how many research files and briefs were generated this run, and clearly call out which brief won and why. Note any key insights from the LinkedIn benchmark that influenced the pipeline.
