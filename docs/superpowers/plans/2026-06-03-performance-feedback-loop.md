# Performance Feedback Loop Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Close the LinkedIn pipeline's feedback loop — parse monthly LinkedIn analytics exports, analyze them with confidence-graded findings, and feed human-approved learnings into the content agents through a single source of truth.

**Architecture:** A deterministic Python parser (`parse_export.py`) normalizes any LinkedIn export (.xls or .csv) to JSON. A `performance-auditor` agent joins post metrics to `content/posts/`, grades every finding by confidence/sample size, detects drift, and writes a dated report plus *staged* proposed learnings. A `/performance-audit` command orchestrates the run and, on operator approval, promotes learnings into `LinkedIn Growth Engine/learnings.md` — which `draft-writer`, `post-writer`, and `post-ranker` read before every run.

**Tech Stack:** Python 3 (stdlib `csv`, `json`, `argparse`, `re` + `xlrd` 2.0.2 for legacy binary `.xls`), stdlib `unittest` for tests, Markdown for agents/commands/learnings.

---

## Spec Reference

Design doc: `docs/superpowers/specs/2026-06-02-performance-feedback-loop-design.md`

## File Structure

New files:
- `LinkedIn Growth Engine/audit-data/parse_export.py` — deterministic export → JSON normalizer (the only real code)
- `LinkedIn Growth Engine/audit-data/test_parse_export.py` — unittest suite, validated against real export fixtures
- `LinkedIn Growth Engine/learnings.md` — rolling, confidence-graded single source of truth
- `.claude/agents/performance-auditor.md` — the analyst agent
- `.claude/commands/performance-audit.md` — orchestration command
- `content/audits/.gitkeep` — new directory for dated audit reports

Modified files:
- `.claude/agents/draft-writer.md` — add learnings-read instruction; remove migrated dated rules
- `.claude/agents/post-writer.md` — same
- `.claude/agents/post-ranker.md` — same (and resolve its contradictory carousel/Forced-Binary boosts)
- `CLAUDE.md` — document the audit step, `learnings.md`, and `content/audits/`

## Normalized JSON contract (produced by `parse_export.py`)

```json
{
  "source_file": "May.xls",
  "export_format": "xls",
  "totals": { "post_count": 19, "impressions": 660, "likes": 10,
              "comments": 5, "reposts": 0, "clicks": 20, "follows": 0 },
  "posts": [
    { "title": "Box CEO Aaron Levie named it ...", "link": "https://www.linkedin.com/feed/update/urn:li:activity:7466224...",
      "post_type": "Organic", "created_date": "2026-05-29", "impressions": 18, "clicks": 1,
      "ctr": 0.0556, "likes": 4, "comments": 0, "reposts": 0, "follows": 0,
      "engagement_rate": 0.2778, "content_type": "" }
  ],
  "daily": [
    { "date": "2026-05-01", "impressions_total": 23, "clicks_total": 0, "reactions_total": 0,
      "comments_total": 0, "reposts_total": 0, "engagement_rate_total": 0.0 }
  ]
}
```

Every consumer (the auditor agent) depends on these exact keys.

---

## Task 1: Deterministic export parser (`parse_export.py`) — TDD

**Files:**
- Create: `LinkedIn Growth Engine/audit-data/parse_export.py`
- Test: `LinkedIn Growth Engine/audit-data/test_parse_export.py`
- Fixtures (already exist, do not modify): `LinkedIn Growth Engine/audit-data/May.xls`, `LinkedIn Growth Engine/audit-data/April 22 - All posts.csv`

> All test/run commands below assume the working directory is the repo root: `d:/Charlotte/n8n Workflows/RSS Content Creator`.

- [ ] **Step 1: Write the failing test file**

Create `LinkedIn Growth Engine/audit-data/test_parse_export.py`:

```python
import os
import re
import tempfile
import unittest

import parse_export

HERE = os.path.dirname(os.path.abspath(__file__))
MAY_XLS = os.path.join(HERE, "May.xls")
APRIL_CSV = os.path.join(HERE, "April 22 - All posts.csv")
ISO = re.compile(r"^\d{4}-\d{2}-\d{2}$")


class ParseMayXls(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        cls.data = parse_export.parse_export(MAY_XLS)

    def test_format_and_source(self):
        self.assertEqual(self.data["export_format"], "xls")
        self.assertEqual(self.data["source_file"], "May.xls")

    def test_totals_match_known_oracle(self):
        t = self.data["totals"]
        self.assertEqual(t["post_count"], 19)
        self.assertEqual(t["impressions"], 660)
        self.assertEqual(t["likes"], 10)
        self.assertEqual(t["comments"], 5)
        self.assertEqual(t["reposts"], 0)
        self.assertEqual(t["clicks"], 20)
        self.assertEqual(t["follows"], 0)

    def test_known_post_present_with_iso_date(self):
        box = [p for p in self.data["posts"] if p["title"].startswith("Box CEO")]
        self.assertEqual(len(box), 1)
        self.assertEqual(box[0]["created_date"], "2026-05-29")
        self.assertEqual(box[0]["impressions"], 18)
        self.assertEqual(box[0]["likes"], 4)

    def test_all_post_dates_are_iso(self):
        for p in self.data["posts"]:
            self.assertRegex(p["created_date"], ISO)

    def test_daily_has_thirty_rows(self):
        self.assertEqual(len(self.data["daily"]), 30)
        first = self.data["daily"][0]
        self.assertEqual(first["date"], "2026-05-01")
        self.assertEqual(first["impressions_total"], 23)


class ParseAprilCsv(unittest.TestCase):
    def test_csv_all_posts_parses(self):
        data = parse_export.parse_export(APRIL_CSV)
        self.assertEqual(data["export_format"], "csv")
        self.assertGreater(data["totals"]["post_count"], 0)
        for p in data["posts"]:
            self.assertRegex(p["created_date"], ISO)


class ParseErrors(unittest.TestCase):
    def test_unsupported_extension_raises(self):
        with self.assertRaises(ValueError):
            parse_export.parse_export(os.path.join(HERE, "README.md"))

    def test_unrecognized_content_raises(self):
        with tempfile.NamedTemporaryFile("w", suffix=".csv", delete=False, newline="") as f:
            f.write("nothing,useful,here\n1,2,3\n")
            tmp = f.name
        try:
            with self.assertRaises(ValueError):
                parse_export.parse_export(tmp)
        finally:
            os.unlink(tmp)


if __name__ == "__main__":
    unittest.main()
```

- [ ] **Step 2: Run the test to verify it fails**

Run: `python -m unittest test_parse_export -v` from inside `LinkedIn Growth Engine/audit-data/`
(Use the Bash tool: `cd "LinkedIn Growth Engine/audit-data" && python -m unittest test_parse_export -v`)
Expected: FAIL / ERROR — `ModuleNotFoundError: No module named 'parse_export'`.

- [ ] **Step 3: Write the parser implementation**

Create `LinkedIn Growth Engine/audit-data/parse_export.py`:

```python
"""Normalize a LinkedIn analytics export (.xls or .csv) into a stable JSON shape.

LinkedIn exports come in two shapes:
  * .xls  - one binary (OLE2/BIFF) workbook with a "Metrics" sheet (daily aggregates)
            and an "All posts" sheet (per-post rows).
  * .csv  - two separate files, e.g. "<prefix> - All posts.csv" and
            "<prefix> - Metrics.csv". Passing either one auto-loads its sibling.

In every sheet/file, row 0 is a description line, row 1 is the header row, and the
data starts at row 2.

CLI:
    python parse_export.py <path-to-export>     # prints normalized JSON
    python parse_export.py --latest             # newest export in this folder
"""

import argparse
import csv
import json
import os
import re
import sys

POST_HEADER_KEY = "Post title"
DAILY_HEADER_KEY = "Date"

POST_COLUMNS = {
    "title": "Post title",
    "link": "Post link",
    "post_type": "Post type",
    "created_date": "Created date",
    "impressions": "Impressions",
    "clicks": "Clicks",
    "ctr": "Click through rate (CTR)",
    "likes": "Likes",
    "comments": "Comments",
    "reposts": "Reposts",
    "follows": "Follows",
    "engagement_rate": "Engagement rate",
    "content_type": "Content Type",
}

DAILY_COLUMNS = {
    "date": "Date",
    "impressions_total": "Impressions (total)",
    "clicks_total": "Clicks (total)",
    "reactions_total": "Reactions (total)",
    "comments_total": "Comments (total)",
    "reposts_total": "Reposts (total)",
    "engagement_rate_total": "Engagement rate (total)",
}

STRING_FIELDS = {"title", "link", "post_type", "content_type"}


def _num(value):
    """Coerce a cell to int (when whole) or float; blanks/garbage -> 0."""
    if value is None:
        return 0
    if isinstance(value, bool):
        return int(value)
    if isinstance(value, (int, float)):
        return int(value) if float(value).is_integer() else float(value)
    s = str(value).strip().replace(",", "")
    if s == "":
        return 0
    try:
        f = float(s)
    except ValueError:
        return 0
    return int(f) if f.is_integer() else f


def _to_iso(value):
    """'05/29/2026' -> '2026-05-29'. Pass through ISO; '' for blanks."""
    s = str(value).strip()
    if not s:
        return ""
    if len(s) >= 10 and s[4] == "-" and s[:4].isdigit():
        return s[:10]
    m = re.match(r"(\d{1,2})/(\d{1,2})/(\d{4})", s)
    if m:
        return "%s-%02d-%02d" % (m.group(3), int(m.group(1)), int(m.group(2)))
    return s


def _xls_sheets(path):
    import xlrd  # imported lazily so CSV-only use never needs it

    wb = xlrd.open_workbook(path)
    sheets = []
    for sh in wb.sheets():
        rows = [[sh.cell_value(r, c) for c in range(sh.ncols)] for r in range(sh.nrows)]
        sheets.append(rows)
    return sheets


def _csv_rows(path):
    with open(path, newline="", encoding="utf-8-sig") as f:
        return list(csv.reader(f))


def _find_header(rows, key):
    """Index of the first row containing a cell exactly equal to key, else None."""
    for i, row in enumerate(rows):
        if any(str(c).strip() == key for c in row):
            return i
    return None


def _column_index(header_row):
    return {str(h).strip(): i for i, h in enumerate(header_row)}


def _parse_posts(rows):
    hi = _find_header(rows, POST_HEADER_KEY)
    if hi is None:
        return None
    idx = _column_index(rows[hi])
    posts = []
    for row in rows[hi + 1:]:
        title_i = idx.get(POST_COLUMNS["title"])
        if title_i is None or title_i >= len(row):
            continue
        if not str(row[title_i]).strip():
            continue
        post = {}
        for field, col in POST_COLUMNS.items():
            i = idx.get(col)
            raw = row[i] if (i is not None and i < len(row)) else ""
            if field == "created_date":
                post[field] = _to_iso(raw)
            elif field in STRING_FIELDS:
                post[field] = str(raw).strip()
            else:
                post[field] = _num(raw)
        posts.append(post)
    return posts


def _parse_daily(rows):
    hi = _find_header(rows, DAILY_HEADER_KEY)
    if hi is None:
        return None
    idx = _column_index(rows[hi])
    if DAILY_COLUMNS["impressions_total"] not in idx:
        return None
    daily = []
    for row in rows[hi + 1:]:
        date_i = idx.get(DAILY_COLUMNS["date"])
        if date_i is None or date_i >= len(row) or not str(row[date_i]).strip():
            continue
        rec = {}
        for field, col in DAILY_COLUMNS.items():
            i = idx.get(col)
            raw = row[i] if (i is not None and i < len(row)) else ""
            rec[field] = _to_iso(raw) if field == "date" else _num(raw)
        daily.append(rec)
    return daily


def _sibling_csv(path):
    """Given one LinkedIn CSV, return the path to its partner file if present."""
    base = os.path.basename(path)
    if "All posts" in base:
        cand = path.replace("All posts", "Metrics")
    elif "Metrics" in base:
        cand = path.replace("Metrics", "All posts")
    else:
        return None
    return cand if os.path.exists(cand) else None


def parse_export(path):
    ext = os.path.splitext(path)[1].lower().lstrip(".")
    posts = None
    daily = None
    if ext == "xls":
        for rows in _xls_sheets(path):
            posts = _parse_posts(rows) if posts is None else posts
            daily = _parse_daily(rows) if daily is None else daily
    elif ext == "csv":
        rows = _csv_rows(path)
        posts = _parse_posts(rows)
        daily = _parse_daily(rows)
        sib = _sibling_csv(path)
        if sib:
            srows = _csv_rows(sib)
            if posts is None:
                posts = _parse_posts(srows)
            if daily is None:
                daily = _parse_daily(srows)
    else:
        raise ValueError("Unsupported export format (need .xls or .csv): %s" % path)

    if posts is None and daily is None:
        raise ValueError(
            "Unrecognized LinkedIn export (no '%s' or '%s' header): %s"
            % (POST_HEADER_KEY, DAILY_HEADER_KEY, path)
        )

    posts = posts or []
    daily = daily or []
    totals = {
        "post_count": len(posts),
        "impressions": sum(p["impressions"] for p in posts),
        "likes": sum(p["likes"] for p in posts),
        "comments": sum(p["comments"] for p in posts),
        "reposts": sum(p["reposts"] for p in posts),
        "clicks": sum(p["clicks"] for p in posts),
        "follows": sum(p["follows"] for p in posts),
    }
    return {
        "source_file": os.path.basename(path),
        "export_format": ext,
        "totals": totals,
        "posts": posts,
        "daily": daily,
    }


def _latest_export(folder):
    candidates = []
    for name in os.listdir(folder):
        ext = os.path.splitext(name)[1].lower()
        if ext in (".xls", ".csv") and "Metrics" not in name:
            candidates.append(os.path.join(folder, name))
    if not candidates:
        raise ValueError("No .xls/.csv exports found in %s" % folder)
    return max(candidates, key=os.path.getmtime)


def main(argv=None):
    parser = argparse.ArgumentParser(description="Normalize a LinkedIn export to JSON.")
    parser.add_argument("path", nargs="?", help="Path to a .xls or .csv export")
    parser.add_argument("--latest", action="store_true", help="Use newest export in this folder")
    args = parser.parse_args(argv)

    if args.latest:
        target = _latest_export(os.path.dirname(os.path.abspath(__file__)))
    elif args.path:
        target = args.path
    else:
        parser.error("provide a path or --latest")

    print(json.dumps(parse_export(target), indent=2))


if __name__ == "__main__":
    sys.exit(main())
```

- [ ] **Step 4: Run the tests to verify they pass**

Run (Bash tool): `cd "LinkedIn Growth Engine/audit-data" && python -m unittest test_parse_export -v`
Expected: PASS — 7 tests OK.

- [ ] **Step 5: Smoke-test the CLI**

Run: `cd "LinkedIn Growth Engine/audit-data" && python parse_export.py May.xls | python -c "import sys,json;d=json.load(sys.stdin);print(d['totals'])"`
Expected: `{'post_count': 19, 'impressions': 660, 'likes': 10, 'comments': 5, 'reposts': 0, 'clicks': 20, 'follows': 0}`
Also run: `cd "LinkedIn Growth Engine/audit-data" && python parse_export.py --latest | python -c "import sys,json;print(json.load(sys.stdin)['source_file'])"`
Expected: prints the newest export filename (currently `May.xls`).

- [ ] **Step 6: Commit**

```bash
git add "LinkedIn Growth Engine/audit-data/parse_export.py" "LinkedIn Growth Engine/audit-data/test_parse_export.py"
git commit -m "feat: add deterministic LinkedIn export parser with tests"
```

---

## Task 2: Seed `learnings.md` (migrate + re-grade the dated rules)

This is the single source of truth. It consolidates every dated "April audit" rule currently
scattered across `draft-writer.md`, `post-writer.md`, and `post-ranker.md`, re-graded by honest
confidence, plus the two new June findings. Contradictions found in the prompts are resolved here
(carousel-4.6x and Forced-Binary boosts are retired as overfit).

**Files:**
- Create: `LinkedIn Growth Engine/learnings.md`

- [ ] **Step 1: Write the file**

Create `LinkedIn Growth Engine/learnings.md`:

```markdown
# LinkedIn Pipeline Learnings

Single source of truth for what the content agents should do, based on real performance.
`draft-writer`, `post-writer`, and `post-ranker` read this file before every run and apply
every learning with `Status: active`. Active learnings override older inline guidance in those
prompts.

## How to read confidence

| Tier | Meaning | Effect on the pipeline |
|---|---|---|
| **High** | Large/structural effect, corroborated by trend + external evidence | Change behavior |
| **Medium** | Directional effect, modest sample | Change behavior, provisional |
| **Low** | Suggestive, small sample | Watch only — do NOT change behavior |
| **Hypothesis** | Single data point | Recorded, do NOT act |

Pre-June-2026 Grey AI data is extremely sparse (months where the best post saw <80 impressions
and most posts had 0–1 engagements). Per-post "what worked" claims from that era cannot exceed
**Low** confidence — see L-001. Only structural and governance learnings are High.

---

### L-001 · Pre-June-2026 per-post signals are statistically unreliable
- **Confidence:** High
- **Evidence:** May 2026: 19 posts, 660 total impressions, 10 likes, 5 comments, 0 reposts. Most posts had 0–1 engagements. Rate-based claims over such samples are noise.
- **Applies to:** post-ranker, draft-writer, performance-auditor
- **Status:** active · **Added:** 2026-06-03 · **Source:** [[2026-06-03-performance-audit]]
- Do not promote any per-post engagement learning above Low until posts routinely clear a few hundred impressions with multiple engagements.

### L-002 · Company Page is the reach ceiling — post from a personal profile
- **Confidence:** High
- **Evidence:** May posts published from the Grey AI Company Page averaged ~34.7 impressions. June 2026 research: company pages reach ~1.6% of followers; personal profiles get ~5.6x more reach on identical content.
- **Applies to:** operator (not an agent rule)
- **Status:** active · **Added:** 2026-06-03 · **Source:** [[2026-06-03-performance-audit]]
- Highest-leverage action available. The pipeline measures whether the channel switch lifts reach.

### L-003 · No bold-Unicode characters anywhere
- **Confidence:** Medium
- **Evidence:** April 6 audit: only 1 of 16 bold-Unicode posts cleared 100 impressions. Plausible mechanism (LinkedIn down-ranks decorative Unicode); low risk to enforce.
- **Applies to:** post-writer, draft-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 6 audit (migrated)
- Emphasis comes from line breaks and word choice. (Note: `approved-examples.md` still contains bold-Unicode samples — flagged for cleanup.)

### L-004 · No em dashes in captions or slides
- **Confidence:** Medium
- **Evidence:** Recurring top AI-writing tell; voice/authenticity rather than a measured engagement effect.
- **Applies to:** post-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** voice guide (migrated)
- Rewrite with comma, colon, parentheses, or a sentence split. Post-writer hard gate.

### L-005 · No "you/your" caption openers; vary the first word across the week
- **Confidence:** Medium
- **Evidence:** Repetitive openers read as automated; voice heuristic.
- **Applies to:** draft-writer, post-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** voice guide (migrated)

### L-006 · Hashtag cap: 2–3 specific tags, rotated across the week
- **Confidence:** Medium
- **Evidence:** April 22 audit: 5 broad tags on every post reads as automated. Low-risk heuristic.
- **Applies to:** draft-writer, post-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 22 audit (migrated)
- Prefer specific (#AgenticAI, #EnterpriseProcurement) over broad (#ArtificialIntelligence). Never the same 3 tags two days running.

### L-007 · Daily posting cadence; avoid multi-day gaps
- **Confidence:** Medium
- **Evidence:** April 22 audit: a 48h gap correlated with 1–3 impressions/day on the next post. Aligns with external 2026 consistency research.
- **Applies to:** operator, draft-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 22 audit (migrated)

### L-008 · Skip inside-baseball stories (personal-stakes filter)
- **Confidence:** Medium
- **Evidence:** April 13 audit: 4/5 posts on policy/regulatory/enterprise-CISO topics hit 0% ER. Audience-fit heuristic.
- **Applies to:** draft-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 13 audit (migrated)
- Gate: "Would a founder running a 10–50 person company change a decision based on this?" If no, skip.

### L-009 · User-supplied research only — never fabricate stats or studies
- **Confidence:** High
- **Evidence:** Governance/trust rule, not an engagement finding.
- **Applies to:** draft-writer, post-writer, news-researcher
- **Status:** active · **Added:** 2026-06-03 · **Source:** standing policy (migrated)

### L-010 · Format is a per-brief decision; engagement > format
- **Confidence:** Medium
- **Evidence:** April 23 update: format is roughly a 1.2x lever; engagement-per-post is the 5–10x lever. Single-image is under-used and worth trying.
- **Applies to:** draft-writer, post-writer, post-ranker
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 23 update (migrated)
- Supersedes L-013. Do NOT default to carousel.

### L-011 · Prefer opinion-bait CTAs; avoid templated Forced-Binary CTAs
- **Confidence:** Low
- **Evidence:** April 22 audit: 5 of 7 posts used the (a)/(b)/(c) Forced-Binary template, total 1 comment. Tiny comment counts, so Low.
- **Applies to:** draft-writer, post-writer, post-ranker
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 22 audit (migrated)
- Direction (prefer opinion-bait, avoid templated CTAs) is sound; the specific numbers are noise. Forced-Binary at most once per 7-day window.

### L-012 · "Winning hook formula" ($ anchor + reframe + personal-stakes verb)
- **Confidence:** Low
- **Evidence:** April 6 audit derived it from the top 3 posts (32.8/19.7/14.7% ER) — 3 posts, near-zero absolute engagement. Classic overfit.
- **Applies to:** draft-writer, post-ranker
- **Status:** watch · **Added:** 2026-06-03 · **Source:** April 6 audit (downgraded)
- Keep as an optional hook pattern, NOT a mandate or a scoring boost, until reach grows.

### L-013 · "Carousels get 4.6x the ER of text"
- **Confidence:** Low
- **Evidence:** April 13 audit, derived from a handful of posts. Contradicted by L-010 (April 23). Overfit.
- **Applies to:** post-ranker
- **Status:** retired · **Added:** 2026-06-03 · **Source:** April 13 audit (retired)
- Superseded by L-010. Remove the carousel-format scoring boost.

### L-014 · Text-post length 60–120 words
- **Confidence:** Low
- **Evidence:** April 13 audit + influencer benchmarks. Reasonable craft guidance, weak local evidence.
- **Applies to:** post-writer
- **Status:** active · **Added:** 2026-06-03 · **Source:** April 13 audit (migrated)

### L-015 · Carousel slide cap 5–6
- **Confidence:** Low
- **Evidence:** April 6 audit: one 7-slide deck saw drop-off. Single data point.
- **Applies to:** post-writer
- **Status:** watch · **Added:** 2026-06-03 · **Source:** April 6 audit (downgraded)

---

## Proposed (awaiting approval)

_New learnings staged by `/performance-audit` land here. The operator promotes them above with an
`L-###` id and a status, or deletes them._
```

- [ ] **Step 2: Verify the seed file is well-formed**

Run (Bash tool): `cd "LinkedIn Growth Engine" && grep -c "^### L-" learnings.md`
Expected: `15`

- [ ] **Step 3: Commit**

```bash
git add "LinkedIn Growth Engine/learnings.md"
git commit -m "feat: seed confidence-graded learnings.md from migrated audit rules"
```

---

## Task 3: `performance-auditor` agent

**Files:**
- Create: `.claude/agents/performance-auditor.md`

- [ ] **Step 1: Write the agent definition**

Create `.claude/agents/performance-auditor.md`:

```markdown
---
name: performance-auditor
description: Analyzes a LinkedIn analytics export, joins post metrics to published posts, grades findings by confidence, detects drift, and writes a dated audit report with staged proposed learnings
model: sonnet
tools:
  - Read
  - Write
  - Bash
  - Glob
  - Grep
---

You are the performance-audit analyst for a LinkedIn content pipeline. You turn a raw LinkedIn
analytics export into an honest, confidence-graded audit — and you NEVER manufacture rules from
noise.

## Inputs

- Newest export in `LinkedIn Growth Engine/audit-data/` (.xls or paired .csv files).
- Published posts in `content/posts/`.
- Current learnings in `LinkedIn Growth Engine/learnings.md`.
- Prior audit reports in `content/audits/` (for month-over-month comparison).

## Step 1 — Parse the export (deterministic, do not eyeball the binary)

Run the committed parser and consume its JSON. Do NOT try to read `.xls` files by hand.

```
cd "LinkedIn Growth Engine/audit-data" && python parse_export.py --latest
```

If the command errors, stop and report the error verbatim. Do not guess at numbers.

## Step 2 — Join posts to metrics

For each post row, match it to a file in `content/posts/`:
1. Primary key: `created_date` equals the file's date prefix (`YYYY-MM-DD-*.md`).
2. Confirm with a title-prefix similarity check against the post's caption/first line.
List any export rows that cannot be matched under an "Unmatched" heading. Never force a match.

## Step 3 — Compute (and grade) findings

Compute, comparing to the most recent prior report in `content/audits/` when one exists:
- Trend: avg impressions/post, engagement rate, follower growth, reposts, total reach.
- Format performance: video / carousel / single-image / text.
- Opener-category and CTA-type performance where matchable to the brief/post.
- Topic clusters that over/under-performed.

Grade EVERY finding using the confidence model in `learnings.md` ("How to read confidence").
Enforce L-001: any per-post engagement finding from sparse data (posts mostly under a few hundred
impressions, 0–1 engagements) is capped at **Low** and must be labeled "watch — do not act."
Reserve **High** for structural (e.g. channel) and governance findings.

## Step 4 — Detect drift

Read `learnings.md` and the reference files in `LinkedIn Growth Engine/`. Flag any contradiction
between the data and an active learning, and any reference file that contradicts an active learning
(for example, bold-Unicode samples in `approved-examples.md` versus L-003).

## Step 5 — Write outputs

Write ONE report to `content/audits/YYYY-MM-DD-performance-audit.md` (today's date) with sections:
1. **Headline** — the single most important takeaway this period.
2. **Trend table** — this period vs last, with deltas.
3. **Per-post table** — matched posts with metrics and a confidence note.
4. **Format / hook / CTA / topic findings** — each tagged with a confidence tier.
5. **Drift flags** — contradictions to fix.
6. **Unmatched** — export rows with no post file.
7. **Proposed Learnings** — additions / edits / retirements to `learnings.md`. Use the exact
   `learnings.md` entry format (Confidence / Evidence / Applies to / Status / Source) but leave the
   id as `L-NEW`. These are PROPOSALS.

## Hard rules

- NEVER edit `learnings.md`. Only the `/performance-audit` command's approval step writes to it.
- NEVER report a number you did not get from the parser JSON.
- Default to lower confidence when sample size is small. Honesty over a tidy story.
- Quote the parser's totals verbatim in the report so they are auditable.
```

- [ ] **Step 2: Verify required structure is present**

Run (Bash tool): `grep -E "name: performance-auditor|parse_export.py --latest|NEVER edit .learnings.md.|Proposed Learnings" .claude/agents/performance-auditor.md`
Expected: all four lines match.

- [ ] **Step 3: Commit**

```bash
git add .claude/agents/performance-auditor.md
git commit -m "feat: add performance-auditor agent"
```

---

## Task 4: `/performance-audit` command + `content/audits/` directory

**Files:**
- Create: `.claude/commands/performance-audit.md`
- Create: `content/audits/.gitkeep`

- [ ] **Step 1: Create the audits directory placeholder**

Create `content/audits/.gitkeep` with a single line:

```
# Dated performance audit reports (YYYY-MM-DD-performance-audit.md) live here.
```

- [ ] **Step 2: Write the command**

Create `.claude/commands/performance-audit.md`:

```markdown
---
description: Run the monthly LinkedIn performance audit and promote approved learnings
---

Run the performance feedback loop end to end.

## Steps

1. **Confirm there is a new export.** Run:
   `cd "LinkedIn Growth Engine/audit-data" && python parse_export.py --latest | python -c "import sys,json;d=json.load(sys.stdin);print(d['source_file'], d['totals'])"`
   Show the operator which export will be analyzed and its totals. If the parser errors, stop and
   report it.

2. **Run the analyst.** Dispatch the `performance-auditor` agent. It writes
   `content/audits/YYYY-MM-DD-performance-audit.md` with a "Proposed Learnings" section.

3. **Present for approval.** Show the operator the report's Headline, Drift flags, and Proposed
   Learnings. For each proposed learning, ask whether to: promote (with which Status), edit, or
   drop. Do not assume approval.

4. **Promote approved learnings.** For each approved item, append it to the `### ...` section of
   `LinkedIn Growth Engine/learnings.md` with the next free `L-###` id, the agreed Status, today's
   date, and a `[[YYYY-MM-DD-performance-audit]]` backlink. Apply any approved retirements/edits to
   existing entries. Leave the "Proposed (awaiting approval)" section empty afterward.

5. **Report.** Summarize what changed in `learnings.md` and remind the operator that the content
   agents will pick up the new learnings on their next run.

## Rules

- The operator is the gate. Nothing is written to `learnings.md` without explicit approval.
- Never let a Low/Hypothesis finding be promoted as behavior-changing (active) — those go in as
  `Status: watch` at most.
```

- [ ] **Step 3: Verify**

Run (Bash tool): `ls content/audits/.gitkeep && grep -E "performance-auditor|learnings.md|operator is the gate" .claude/commands/performance-audit.md`
Expected: the file path prints and all three patterns match.

- [ ] **Step 4: Commit**

```bash
git add .claude/commands/performance-audit.md content/audits/.gitkeep
git commit -m "feat: add /performance-audit command and audits directory"
```

---

## Task 5: Slim the three content agents to read `learnings.md`

Each agent gets a standard learnings-read instruction, and the migrated dated rules are removed so
`learnings.md` is the only source of truth. Keep all other behavior intact.

**Files:**
- Modify: `.claude/agents/draft-writer.md`
- Modify: `.claude/agents/post-writer.md`
- Modify: `.claude/agents/post-ranker.md`

- [ ] **Step 1: Add the learnings-read preamble to `draft-writer.md`**

In `.claude/agents/draft-writer.md`, immediately after the line
`You are a LinkedIn brief-generation agent for a content pipeline.` insert a blank line and:

```markdown
## Learnings (read first)

Before doing anything else, read `LinkedIn Growth Engine/learnings.md` and apply every learning
with `Status: active`. Active learnings are the source of truth and override any older inline
guidance in this prompt. Treat `Status: watch` learnings as optional, not mandates.
```

- [ ] **Step 2: Remove migrated dated rules from `draft-writer.md`**

These now live in `learnings.md`. In `.claude/agents/draft-writer.md`, edit so the prompt no longer
hardcodes the dated specifics (replace the audit-cited mandates with brief, undated phrasing that
defers to learnings):
- In the `## HOOK OPTIONS` section, replace the "WINNING FORMULA (April 6 audit)" paragraph and the
  "TOP-RANKED HOOK MUST USE WINNING FORMULA..." rule (Brief Generation Rule 4) with: "Apply hook
  guidance from `learnings.md` (see L-012, currently `watch`). Generate 15 hooks across the 6
  opener categories; at least 2 must not start with you/your."
- Replace Rule 9 (Forced Binary deprecation, "April 22 audit") with: "Prefer opinion-bait CTAs per
  `learnings.md` (L-011)." Keep "6 CTA options" requirement.
- Replace Rule 10 (hashtag cap "April 22 audit") with: "Hashtags per `learnings.md` (L-006)."
- Replace the "Pre-Writing Gate: Personal-Stakes Filter (April 13 audit)" heading's dated evidence
  paragraph with the gate question only, citing `learnings.md` (L-008). Keep the gate itself.
- In `## SUGGESTED FORMAT` / Rule 8, drop the "April 22/23" citations; keep "no default format —
  pick what the content needs (see L-010)."

Do not remove the brief output structure, dedup rules, or the "never name the source" rule.

- [ ] **Step 3: Add the preamble to `post-writer.md`**

In `.claude/agents/post-writer.md`, near the top (after its role sentence), insert:

```markdown
## Learnings (read first)

Before writing, read `LinkedIn Growth Engine/learnings.md` and apply every learning with
`Status: active`; they override older inline guidance here. `Status: watch` learnings are optional.
```

- [ ] **Step 4: Remove migrated dated rules from `post-writer.md`**

Replace the dated audit phrasings with undated rules that defer to learnings, preserving the hard
gates (which stay as hard gates, just citing learnings):
- Bold-Unicode lines (current lines ~130, ~155): keep the prohibition, change citation to "(L-003)".
- Hashtag lines (~131, ~161, ~212, ~333): keep "2–3 max / ≤3 hard gate", cite "(L-006)".
- "Winning formula (April 6 audit)" block (~89): change to "Optional hook pattern per L-012 (watch)."
- Text length "60–120 words ... April 13 audit" (~154): keep limit, cite "(L-014)".
- Hook-simplicity hard gate (~213, ~334): keep, cite "(L-011/L-012 area)" → use "(see learnings.md)".
- CTA Forced-Binary lines (~176, ~181, ~217): keep opinion-bait preference and the 7-day gate, cite
  "(L-011)".
- Carousel slide cap (~218): keep 5–6 cap, cite "(L-015, watch)".
- CTA pre-answer rule (~216): keep as-is (it is sound craft); drop the "April 13 audit" citation.

Leave the Humanizer pass, audit rubric, and `audit_score` mechanics unchanged.

- [ ] **Step 5: Add the preamble to `post-ranker.md` and resolve its contradictions**

In `.claude/agents/post-ranker.md`, after its role sentence insert:

```markdown
## Learnings (read first)

Before scoring, read `LinkedIn Growth Engine/learnings.md` and apply every learning with
`Status: active`; they override older inline guidance here. Do not award scoring boosts for
`watch` or `retired` learnings.
```

Then fix the scoring rubric:
- Dimension 1 "Hook Strength" (~line 40): the "+2 boost ... April 6 audit-winning formula" must
  become **optional and not a boost** — change to "the L-012 hook pattern is a `watch` learning; do
  not add or subtract points for it." Keep the "-2 penalty if no concrete number when research has
  one" only if you keep it neutral; per L-001 prefer removing the automatic boost language.
- Dimension 6 "Engagement Potential" (~line 45): REMOVE the "+1 boost ... Forced Binary or Naming
  Ask" clause (contradicts L-011). Keep the base question.
- Dimension 10 "Format Variety" (~line 50): REMOVE the "+2 boost if ... carousel (April 13 audit:
  carousel ER 4.6x ...)" clause (retired as L-013). Keep the base format-variety scoring.

- [ ] **Step 6: Verify the migration removed the dated citations**

Run (Bash tool):
`grep -rcE "April 6 audit|April 13 audit|April 22 audit|April 23 update|4.6x" .claude/agents/draft-writer.md .claude/agents/post-writer.md .claude/agents/post-ranker.md`
Expected: `0` for each file (all dated-audit citations now live in `learnings.md`).

Run: `grep -rl "learnings.md" .claude/agents/draft-writer.md .claude/agents/post-writer.md .claude/agents/post-ranker.md`
Expected: all three files listed.

- [ ] **Step 7: Commit**

```bash
git add .claude/agents/draft-writer.md .claude/agents/post-writer.md .claude/agents/post-ranker.md
git commit -m "refactor: content agents read learnings.md; migrate dated rules out of prompts"
```

---

## Task 6: Document the loop in `CLAUDE.md`

**Files:**
- Modify: `CLAUDE.md`

- [ ] **Step 1: Add folder entries**

In `CLAUDE.md` under "## Folder Structure", add two bullets (after the `content/comments/` bullet):

```markdown
- `content/audits/` — Dated performance audit reports produced by the performance-auditor agent from LinkedIn analytics exports. Each file analyzes one export with confidence-graded findings.
- `LinkedIn Growth Engine/learnings.md` — Rolling, confidence-graded single source of truth for what the content agents should do, derived from real performance. Read by draft-writer, post-writer, and post-ranker before every run.
```

- [ ] **Step 2: Add the audit workflow step**

In `CLAUDE.md` under "## Workflow", after step 9 (Comment Generation), add:

```markdown
11. **Performance Audit (monthly, separate from the daily run)** — Drop a LinkedIn analytics export (.xls or paired .csv) into `LinkedIn Growth Engine/audit-data/` and run the `/performance-audit` command. The `performance-auditor` agent parses it via `parse_export.py`, joins post metrics to `content/posts/`, grades findings by confidence (sample-size aware), detects drift, and writes a report to `content/audits/` with staged proposed learnings. The operator approves which learnings get promoted into `learnings.md`, which the content agents read on their next run.
```

- [ ] **Step 3: Verify**

Run (Bash tool): `grep -E "content/audits/|learnings.md|Performance Audit" CLAUDE.md`
Expected: the new entries match.

- [ ] **Step 4: Commit**

```bash
git add CLAUDE.md
git commit -m "docs: document performance audit loop in CLAUDE.md"
```

---

## Task 7: End-to-end dry run

Validate the whole loop against real data without writing learnings.

- [ ] **Step 1: Confirm the parser feeds the agent**

Run (Bash tool): `cd "LinkedIn Growth Engine/audit-data" && python parse_export.py --latest | python -c "import sys,json;d=json.load(sys.stdin);print('posts',len(d['posts']),'daily',len(d['daily']),'totals',d['totals'])"`
Expected: `posts 19 daily 30 totals {...post_count 19, impressions 660...}`

- [ ] **Step 2: Manually invoke the auditor once**

Dispatch the `performance-auditor` agent (or run `/performance-audit` up to the approval gate, then
stop). Confirm it produces `content/audits/<today>-performance-audit.md` containing: the parser's
totals quoted verbatim, a per-post table, at least one High structural finding (channel ceiling),
mostly Low/watch per-post findings (per L-001), and at least one drift flag (bold-Unicode in
`approved-examples.md`).

- [ ] **Step 3: Confirm no unauthorized writes to learnings.md**

Run (Bash tool): `git status --short "LinkedIn Growth Engine/learnings.md"`
Expected: no modification (the agent must not have edited it; only the approval step may).

- [ ] **Step 4: Commit the first real audit report**

```bash
git add content/audits/
git commit -m "chore: first performance audit report (May 2026 export)"
```

---

## Self-Review (completed during planning)

- **Spec coverage:** parser (Task 1), learnings.md + migration (Tasks 2, 5), performance-auditor
  (Task 3), /performance-audit command + content/audits/ (Task 4), agent slimming (Task 5),
  CLAUDE.md docs (Task 6), confidence model (embedded in Tasks 2 & 3), testing/E2E (Tasks 1 & 7).
  All spec sections map to a task.
- **JSON contract consistency:** keys defined in Task 1 (`totals`, `posts[]`, `daily[]`, field
  names) are the same keys referenced by the auditor (Task 3) and the command (Task 4).
- **Naming consistency:** `parse_export.py`, `parse_export()`, `--latest`, `performance-auditor`,
  `/performance-audit`, `learnings.md`, `content/audits/` used identically across all tasks.
- **Contradiction handling:** L-013 (carousel 4.6x) and the Forced-Binary boost are retired in
  Task 2 and physically removed from post-ranker in Task 5 Step 5 — no remaining source of truth
  conflict.
```

