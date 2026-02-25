---
description: Scrape RSS feeds for research then generate LinkedIn drafts
---

Run the full LinkedIn content pipeline:

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

The agent should read the keywords file from `content/seo/` to guide story selection — prioritizing stories that align with trending topics. It must sort all feed items by publication date (newest first) so the most recent stories are always covered. Save research summaries to `content/research/`.

## Stage 3: Drafting

Once research is complete, use the `draft-writer` subagent to create LinkedIn post drafts from any new research files that don't already have a matching draft.

The agent should read the keywords file from `content/seo/` and save drafts to `content/drafts/`.

## Stage 4: Ranking

Once all drafts are written, use the `post-ranker` subagent to score every draft against the scroll-stopping checklist, rank them, and pick the winner.

The agent should write a ranking report to `content/drafts/_ranking.md` and update each draft's frontmatter status (`winner` for the top pick, `ranked` for the rest).

## Stage 5: Compilation

Once ranking is complete, use the `content-compiler` subagent to compile all of today's ranked drafts and their source research into a single review file.

The agent reads the ranking from `content/drafts/_ranking.md`, pairs each draft with its research file in rank order, and writes the compilation to `content/google doc/YYYY-MM-DD.md` for review in Google Docs.

## Stage 6: Report

After all stages are done, list what was created:

1. SEO keywords file in `content/seo/`
2. New files in `content/research/`
3. New files in `content/drafts/`
4. The ranking results — show the full scoreboard and announce the winner
5. Compilation file in `content/google doc/`

Summarize how many research files and drafts were generated this run, and clearly call out which post won and why.
