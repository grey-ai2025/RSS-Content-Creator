# LinkedIn Content Pipeline

This project is a LinkedIn content pipeline that generates professional posts and image prompts from RSS news feeds. It uses Claude Code agents to automate the full content creation process, leaving final review and publishing to the human operator.

## Folder Structure

- `content/seo/` — Daily keyword research files produced by the seo-researcher agent. Each file contains trending topics, high-impact phrases, and hashtags for LinkedIn optimization.
- `content/research/` — Curated news summaries produced by the news-researcher agent. Each file covers a single story with a structured summary, key data points, and relevance notes.
- `content/drafts/` — LinkedIn post briefs produced by the draft-writer agent. Each file contains a structured brief with YAML frontmatter tracking its source and status. `_ranking.md` contains the scoreboard and winner selection.
- `content/benchmarks/` — LinkedIn influencer benchmark files produced by the linkedin-analyzer agent. Each file contains top-performing post analysis and engagement patterns from leading AI/tech influencers.
- `content/google doc/` — Daily compilation files pairing ranked briefs with their source research, formatted for Google Docs review.
- `content/posts/` — Finished LinkedIn posts produced by the post-writer agent. Each file contains a publish-ready caption and full slide content (or text post body), with audit score and checklist.
- `content/image-prompts/` — Gemini image prompts produced by the image-prompt-generator agent. Each file contains ready-to-paste prompts for Google AI Studio, one per carousel slide or one for a single image.
- `.claude/agents/` — Agent definitions (linkedin-analyzer, seo-researcher, news-researcher, draft-writer, post-ranker, content-compiler, post-writer, image-prompt-generator).
- `.claude/commands/` — Slash commands for running the pipeline.
- `LinkedIn Growth Engine/` — Reference files for the post-writer agent: brand voice, performance benchmarks, carousel templates, post formulas, and audit rubric.
- `Script to Image/` — Reference files for the image-prompt-generator agent: brand rules, image prompt workflows, and imageConfig.json with colors, typography, and layout specs.

## Workflow

1. **LinkedIn Benchmark** — The `linkedin-analyzer` agent uses Firecrawl browser automation to scrape top AI/tech influencer LinkedIn profiles, identifies highest-performing posts, and extracts engagement patterns (hook styles, formats, topics). Falls back to `firecrawl_search` after two browser failures per profile. Saves a benchmark file to `content/benchmarks/`.
2. **SEO Keywords** — The `seo-researcher` agent uses Google Trends MCP tools (`google-news-trends`) as its primary data source, supplemented by web searches for LinkedIn-specific hashtag and engagement data. Saves a structured keywords file to `content/seo/`.
3. **Research** — The `news-researcher` agent scrapes configured RSS feeds via the `rss-reader` MCP server, using WebFetch for full-article scraping, then filters results to only cover stories that match trending keywords from the SEO stage (with an exception for up to 2 exceptionally newsworthy stories). Saves structured research summaries to `content/research/`.
4. **Drafting** — The `draft-writer` agent reads new research files, the SEO keywords file, and LinkedIn benchmark data, then creates original LinkedIn post briefs. Posts never mention source publications or articles — the research informs the content but the reader should never know where it came from. Saves briefs to `content/drafts/`.
5. **Ranking** — The `post-ranker` agent scores every brief against a 10-point scroll-stopping checklist (calibrated against LinkedIn benchmark data), ranks them, and picks the winner.
6. **Compilation** — The `content-compiler` agent reads the ranking, pairs each brief with its source research in rank order, and writes a single compilation file to `content/google doc/` for easy review and copy-paste into Google Docs.
7. **Post Writing** — The `post-writer` agent reads the winning brief and all `LinkedIn Growth Engine/` reference files, applies the Growth Engine workflow and 6-dimension audit rubric (minimum 20/30), and writes a finished LinkedIn post (carousel slides + caption, or text post) to `content/posts/`.
8. **Image Prompts** — The `image-prompt-generator` agent reads the finished post and all `Script to Image/` reference files, selects a visual theme, and writes ready-to-paste Gemini prompts to `content/image-prompts/`.
9. **Review & Publish** — Review the finished post in `content/posts/`, paste the Gemini prompts from `content/image-prompts/` into Google AI Studio to generate images, add the Grey AI logo overlay in Canva, and post manually to LinkedIn.

Run the full pipeline with the `/generate-content` command.

## File Naming Convention

All files in `content/seo/`, `content/research/`, `content/drafts/`, and `content/posts/` follow the pattern:

```
YYYY-MM-DD-slug.md
```

For example: `2026-02-25-openai-launches-new-model.md`

Files in `content/google doc/` and `content/image-prompts/` use date-only naming:

```
YYYY-MM-DD.md
```

## Pipeline Output

The pipeline produces a finished LinkedIn post and matching Gemini image prompts each run:

- `content/posts/YYYY-MM-DD-<slug>.md` — Finished post with caption, slides (or text body), and audit score
- `content/image-prompts/YYYY-MM-DD.md` — Gemini prompts to paste into Google AI Studio

After generating images, overlay the Grey AI logo PNG at top-right (x=820, y=20, max-width 200px) in Canva or Figma before publishing.
