# LinkedIn Content Pipeline

This project is a LinkedIn content pipeline that generates professional post drafts from RSS news feeds. It uses Claude Code agents to automate the research and drafting stages, leaving final review and publishing to the human operator.

## Folder Structure

- `content/seo/` — Daily keyword research files produced by the seo-researcher agent. Each file contains trending topics, high-impact phrases, and hashtags for LinkedIn optimization.
- `content/research/` — Curated news summaries produced by the news-researcher agent. Each file covers a single story with a structured summary, key data points, and relevance notes.
- `content/drafts/` — LinkedIn post drafts produced by the draft-writer agent. Each file contains a ready-to-review post with YAML frontmatter tracking its source and status. `_ranking.md` contains the scoreboard and winner selection.
- `content/benchmarks/` — LinkedIn influencer benchmark files produced by the linkedin-analyzer agent. Each file contains top-performing post analysis and engagement patterns from leading AI/tech influencers.
- `content/google doc/` — Daily compilation files pairing ranked drafts with their source research, formatted for Google Docs review.
- `.claude/agents/` — Agent definitions (linkedin-analyzer, seo-researcher, news-researcher, draft-writer, post-ranker, content-compiler).
- `.claude/commands/` — Slash commands for running the pipeline.

## Workflow

1. **LinkedIn Benchmark** — The `linkedin-analyzer` agent scrapes top AI/tech influencer LinkedIn profiles via Firecrawl MCP, identifies highest-performing posts, and extracts engagement patterns (hook styles, formats, topics). Saves a benchmark file to `content/benchmarks/`.
2. **SEO Keywords** — The `seo-researcher` agent uses Google Trends MCP tools (`google-news-trends`) as its primary data source, supplemented by web searches and Firecrawl for LinkedIn-specific hashtag and engagement data. Saves a structured keywords file to `content/seo/`.
3. **Research** — The `news-researcher` agent scrapes configured RSS feeds via the `rss-reader` MCP server, using Firecrawl for enhanced full-article scraping, then filters results to only cover stories that match trending keywords from the SEO stage (with an exception for up to 2 exceptionally newsworthy stories). Saves structured research summaries to `content/research/`.
4. **Drafting** — The `draft-writer` agent reads new research files, the SEO keywords file, and LinkedIn benchmark data, then creates original LinkedIn posts written as thought leadership. Posts never mention source publications or articles — the research informs the content but the reader should never know where it came from. Saves drafts to `content/drafts/`.
5. **Ranking** — The `post-ranker` agent scores every draft against a 10-point scroll-stopping checklist (calibrated against LinkedIn benchmark data), ranks them, and picks the winner.
6. **Compilation** — The `content-compiler` agent reads the ranking, pairs each draft with its source research in rank order, and writes a single compilation file to `content/google doc/` for easy review and copy-paste into Google Docs.
7. **Review & Publish** — I review the top-ranked draft, edit as needed, and post manually to LinkedIn.

Run the full pipeline with the `/generate-content` command.

## File Naming Convention

All files in `content/seo/`, `content/research/`, and `content/drafts/` follow the pattern:

```
YYYY-MM-DD-slug.md
```

For example: `2026-02-25-openai-launches-new-model.md`

## Pipeline Output

This pipeline outputs LinkedIn **briefs**, not finished posts. Briefs contain structured ingredients (headline, key facts, Grey AI angle, 3 hook options, format recommendation, keywords, raw material) designed to be pasted into the Claude.ai "LinkedIn Growth Engine" Project for final post creation and optimization.

The brief format is intentional: research and angle identification happen here in Claude Code. Creative writing, hook selection, carousel design, and engagement optimization happen in the Claude.ai Project which has access to Grey AI's performance benchmarks, carousel templates, post formulas, and audit rubrics.
