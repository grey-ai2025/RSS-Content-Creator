# Performance Feedback Loop — Design

**Date:** 2026-06-02
**Status:** Approved (design); pending implementation plan
**Author:** Grey AI + Claude

## Background

The LinkedIn content pipeline (see `CLAUDE.md`) generates and ships posts daily, but it has no
automated feedback loop. Real performance data — LinkedIn analytics exports such as
`LinkedIn Growth Engine/audit-data/May.xls` — is never fed back into the agents. Every "learning"
today is a manual human audit, hand-coded into agent prompts as dated rules
("April 6 audit", "April 13 audit", "April 22 audit", "April 23 update" in `draft-writer.md`).

Two problems with the status quo:

1. **No compounding.** The system does not get smarter on its own; a human must read each export
   and edit prompts by hand.
2. **Overfitting to noise.** May 2026 had 19 posts, 660 total impressions, 10 likes, 5 comments,
   0 reposts, 0 new followers — averaging ~34.7 impressions/post. At that scale, per-post
   "what worked" signals are statistically meaningless, yet the pipeline has been turning single
   posts (e.g. one 71.2%-ER post) into hard rules. The reference files have also drifted from the
   learnings (e.g. `approved-examples.md` still showcases bold-Unicode hooks that memory records
   as reach-suppressing).

### Important context discovered during design

May's posts were published from the **Grey AI Company Page**, not Kurt Castro's personal profile.
Per June 2026 research, LinkedIn throttles company-page organic reach to ~1.6% of followers and
personal profiles get ~5.6x more reach on identical content. The single highest-leverage growth
action is switching the primary posting channel to a personal profile. **That is an operator
action, out of scope for this build.** This feedback loop's job is to *measure* whether that switch
(and other changes) actually moves the numbers.

## Goal

Close the loop: ingest real LinkedIn performance monthly, analyze it *honestly* (every finding
graded by confidence/sample size), and feed approved learnings into the content agents through a
single source of truth — so the pipeline improves over time without manufacturing rules from noise.

## Non-Goals (YAGNI)

- Auto-pulling analytics via browser automation (brittle, against LinkedIn ToS).
- Weekly/real-time cadence (monthly manual export is the agreed input).
- Charts, dashboards, or a web UI.
- Auto-applying learnings without human approval.
- Switching the posting channel or any other operator action — code measures, humans act.
- A separate Obsidian app dependency. Learnings are plain markdown with `[[backlinks]]`, so an
  Obsidian vault can sit on top for free, but nothing requires it.

## Design Decisions (from brainstorming)

| Decision | Choice |
|---|---|
| Input & cadence | Manual LinkedIn export (.xls/.csv) dropped into `audit-data/`, run ~monthly |
| Learning propagation | Central `learnings.md`, human-approved, read by agents before every run |
| Existing April rules | Migrated into `learnings.md` (re-graded by honest confidence), removed from prompts |
| Analysis engine | Deterministic Python parser + LLM agent analyst |

## Architecture

```
LinkedIn export (.xls/.csv)               operator drops into audit-data/ monthly
        │
        ▼
parse_export.py            deterministic: normalize any LinkedIn export → clean JSON
        │
        ▼
performance-auditor agent  join posts↔metrics, compute trends + CONFIDENCE tiers,
        │                  detect drift vs current learnings/reference files
        ├──────────────▶ content/audits/YYYY-MM-DD-performance-audit.md   (full report)
        └──────────────▶ PROPOSED learnings block (staged, NOT applied)
        │
        ▼
operator approves / edits          human gate
        │
        ▼
LinkedIn Growth Engine/learnings.md   rolling, confidence-graded source of truth
        │
        ▼
draft-writer / post-writer / post-ranker read learnings.md before every run
```

## Components

### 1. `parse_export.py` (committed to `LinkedIn Growth Engine/audit-data/`)

Deterministic Python. Dependencies already present: `xlrd` 2.0.2 (reads legacy binary `.xls`,
which is the LinkedIn export format — OLE2/BIFF), and stdlib `csv` for CSV exports.

- Detects and parses both LinkedIn sheet layouts:
  - **"Metrics"** sheet — daily aggregate (impressions organic/sponsored/total, clicks, reactions,
    comments, reposts, engagement rate).
  - **"All posts"** sheet — per-post (title, link, created date, impressions, clicks, CTR, likes,
    comments, reposts, follows, engagement rate, content type).
- Emits normalized JSON to stdout (or a file): `{ source_file, export_format, daily: [...],
  posts: [...], totals: {...} }`. Numbers coerced to int/float; dates normalized to `YYYY-MM-DD`.
- Fails loudly (non-zero exit + clear message) on unrecognized format or missing expected columns.
- CLI: `python parse_export.py <path-to-export>` (and an optional `--latest` that picks the most
  recently modified export in `audit-data/`).

### 2. `performance-auditor` agent (`.claude/agents/performance-auditor.md`)

Tools: Read, Write, Bash, Glob, Grep. Model: sonnet (consistent with other analysis agents).

Steps:
1. Identify the newest unprocessed export in `audit-data/` (compare against the most recent file in
   `content/audits/`).
2. Run `parse_export.py` via Bash; consume the JSON.
3. **Join** per-post metrics to `content/posts/` files: primary key = created date; confirm via
   title-prefix similarity against the post caption/first line. List any unmatched posts explicitly
   rather than guessing. (Optional enhancement: write the matched LinkedIn activity link into the
   post file's frontmatter on first match for exact future joins.)
4. **Compute**:
   - Month-over-month trend vs the previous audit: avg impressions/post, engagement rate,
     follower growth, reposts, total reach.
   - Format performance: video / carousel / single-image / text.
   - Opener-category and CTA-type performance where matchable to briefs/posts.
   - Topic clusters (which themes over/under-performed).
5. **Grade** every finding with a confidence tier (see model below) driven by sample size and
   absolute engagement, not just rate.
6. **Detect drift**: flag any reference file or existing learning that contradicts the data
   (e.g. bold-Unicode examples in `approved-examples.md`).
7. **Write outputs**:
   - `content/audits/YYYY-MM-DD-performance-audit.md` — full human-readable report.
   - A **"Proposed Learnings"** section within the report: proposed additions / edits / retirements
     to `learnings.md`, each with confidence + evidence. The agent NEVER edits `learnings.md`
     directly.

### 3. `learnings.md` (`LinkedIn Growth Engine/learnings.md`) — new single source of truth

Rolling, curated, confidence-graded. Obsidian-compatible (plain markdown + `[[backlinks]]`).
Entry format:

```markdown
### L-012 · Video out-reaches text ~2x
- **Confidence:** Medium
- **Evidence:** May 2026: video avg 46 imp (n=3) vs text avg 31 (n=14)
- **Applies to:** draft-writer (format), post-ranker
- **Status:** active   · **Added:** 2026-06-02 · **Source:** [[2026-06-02-performance-audit]]
```

- IDs (`L-001`...) are stable handles for cross-reference.
- `Status: active | watch | retired`. Only `active` learnings change agent behavior.
- Seeded by migrating the existing April rules from the agent prompts, each re-graded honestly
  (several drop to Low/Watch given tiny samples).

### 4. Agent slimming

`draft-writer.md`, `post-writer.md`, `post-ranker.md` each gain one standard instruction near the
top:

> Before working, read `LinkedIn Growth Engine/learnings.md` and apply every learning with
> `Status: active`. Active learnings override any older inline guidance in this prompt.

The scattered dated April rules are removed from these prompts and relocated into `learnings.md`
as seed entries. (Net effect: prompts get shorter and stop drifting from the learnings.)

### 5. `/performance-audit` command (`.claude/commands/performance-audit.md`)

Orchestrates the loop:
1. Run `parse_export.py --latest`.
2. Spawn the `performance-auditor` agent.
3. Present the report + proposed learnings to the operator.
4. On approval (with any edits), promote the approved learnings into `learnings.md`
   (assign IDs, set status, add backlink to the audit report).

## Confidence Model (anti-overfitting core)

| Tier | Bar | Pipeline action |
|---|---|---|
| **High** | Large/structural effect, corroborated by trend + external evidence (e.g. company-page reach ceiling) | Change behavior |
| **Medium** | Directional effect, modest sample | Change behavior, marked provisional |
| **Low** | Suggestive, small sample | "Watch" only — no behavior change |
| **Hypothesis** | Single data point | Recorded, explicitly do-not-act |

Thresholds are sample-size-and-absolute-engagement aware: a finding based on rate alone over a
handful of posts with near-zero absolute engagement cannot exceed Low. This is what prevents a
single high-ER post from becoming a rule.

## Data Flow Details — Post↔Metrics Join

- `content/posts/` filenames: `YYYY-MM-DD-slug.md`. Export rows carry a Created date
  (`MM/DD/YYYY`), a title (first ~60 chars of the caption), and a post link
  (`urn:li:activity:...`).
- Match by normalized date first; confirm with title-prefix similarity against the post's caption.
- Unmatched rows (e.g. reshares, or posts created outside the pipeline) are reported, never forced.

## Error Handling

- Parser: unrecognized format / missing columns → non-zero exit + explicit message; the agent
  surfaces this instead of proceeding.
- Both `.xls` and `.csv` supported; both sheet layouts supported.
- Unmatchable posts listed in the report under "Unmatched".
- Low-confidence and Hypothesis findings never auto-promote and never change agent behavior.
- The agent must not edit `learnings.md`; only the command's approval step writes to it.

## Testing Strategy

- **Parser correctness:** run against existing fixtures in `audit-data/` (April CSVs, `May.xls`,
  older `.xls` files). `May.xls` is a known oracle: 19 posts, 660 total impressions, 10 likes,
  5 comments, 0 reposts. Assert these.
- **Join correctness:** confirm `May.xls` post rows match their `content/posts/` files by date;
  confirm the count of unmatched rows is explainable.
- **Confidence behavior:** running the auditor on May's sparse data should yield mostly
  Low/Hypothesis findings plus the one High structural finding (channel ceiling), not a stack of
  confident per-post rules.
- **Migration:** after seeding `learnings.md` from the April rules, the three agents reference it
  and no longer contain the inline dated rules.

## File Inventory

New:
- `LinkedIn Growth Engine/audit-data/parse_export.py`
- `.claude/agents/performance-auditor.md`
- `.claude/commands/performance-audit.md`
- `LinkedIn Growth Engine/learnings.md`
- `content/audits/` (new directory; first report `content/audits/2026-06-02-performance-audit.md`)

Modified:
- `.claude/agents/draft-writer.md` — add learnings-read instruction; remove migrated April rules
- `.claude/agents/post-writer.md` — same
- `.claude/agents/post-ranker.md` — same
- `CLAUDE.md` — document the audit step and new folders

## Open Questions

None blocking. Optional future enhancement: writing the matched LinkedIn activity link back into
post frontmatter for exact future joins.
