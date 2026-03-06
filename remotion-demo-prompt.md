# Remotion Product Demo — Paste This Into Your Remotion Project

Build a Remotion product demo video (1920x1080, 30fps, ~90-120 seconds) showcasing an automated LinkedIn content pipeline built entirely in Claude Code. The video tells the story of how one slash command triggers 5 AI agents that chain together to transform raw news into ranked LinkedIn briefs — with zero custom code.

Use the real data examples below exactly as written — these are actual outputs from the pipeline.

---

## Design System

**Color palette:**
- Background: #0D0D0D (near-black)
- Primary accent: #D4A574 (warm gold — Grey AI brand)
- Secondary accent: #7C8CFF (soft blue for data/tech elements)
- Text: #F5F5F5 (off-white)
- Muted text: #888888
- Success/winner: #4ADE80 (green)
- Agent nodes: #1A1A2E (dark card backgrounds) with #D4A574 borders
- Terminal green: #00FF41 (for CLI text)

**Typography:**
- Headings: Inter Bold or JetBrains Mono Bold
- Body: Inter Regular
- Code/terminal: JetBrains Mono or Fira Code

**Motion principles:**
- Smooth spring animations (stiffness: 100, damping: 20)
- Elements enter from slight offset with opacity fade
- Data flows visualized as animated particles/dots traveling along connection lines
- Staggered reveals for lists (50-80ms delay per item)
- No hard cuts — crossfades or wipe transitions between scenes

---

## Scene 1: The Problem (0s - 12s)

**Visual:** Split screen showing a content creator's chaotic workflow.

Left side — animate these tabs/windows appearing one by one, stacking messily:
- "Google Trends" browser tab
- "TechCrunch" tab
- "Wired AI" tab
- "MIT Tech Review" tab
- A notes app with scattered bullet points
- A LinkedIn compose window (empty)

Right side — a clock or timer counting up:
```
Reading news:        45 min
Researching angles:  30 min
Writing draft:       40 min
SEO optimization:    15 min
───────────────────────────
Total: 2+ hours/day
```

Times animate in one by one. Total pulses red.

**Text overlay (fade in at end):** "What if one command did all of this?"

---

## Scene 2: One Command (12s - 20s)

**Visual:** Clean terminal window centered on screen. Dark background, monospace font, blinking cursor.

Animate typing character by character:
```
$ /generate-content
```

Cursor blinks twice after Enter, then terminal fades and the pipeline visualization begins building.

---

## Scene 3: Pipeline Overview (20s - 30s)

**Visual:** Horizontal pipeline diagram building left to right. Five connected nodes with glowing particles traveling the connections.

```
[SEO Research] ──→ [News Research] ──→ [Brief Writer] ──→ [Ranker] ──→ [Compiler]
```

Each node is a rounded rectangle with:
- Agent icon at top
- Agent name in bold
- "Claude Sonnet" in small muted text

Below the pipeline: **"5 agents. Zero code. One command."**

First node pulses to indicate activation.

---

## Scene 4: Stage 1 — SEO Keywords (30s - 42s)

**Visual:** SEO Research node expands. Data flows IN from sources on the left:

Sources (animate connecting):
- "Google Trends API"
- "LinkedIn Hashtag Data"
- "AI/Tech Topic Signals"

Agent processes (subtle thinking animation), then OUTPUT appears as a file card:

```
📄 2026-03-04-keywords.md

Trending Topics (12)
├─ Anthropic vs. Pentagon / Military AI Ethics
├─ AI Safety Race / Guardrails Loosening
├─ AI Agents as Enterprise Infrastructure
├─ AI Agent Security Vulnerabilities
├─ Small Open-Source Models Beating Proprietary
├─ Context Engineering / Model Context Protocol
└─ ... +6 more

High-Impact Phrases (10)
├─ "the race to the bottom on safety"
├─ "agents are infrastructure now"
├─ "context engineering, not prompt engineering"
├─ "your content's new audience is an LLM"
└─ ... +6 more

Hashtags (15)
├─ #AI (6M+ followers)
├─ #AIAgents (trending)
├─ #AISafety (surging)
├─ #FutureOfWork (1M+ followers)
└─ ... +11 more
```

**Label:** "The control signal — every downstream agent reads this file"

Particle flies toward next stage.

---

## Scene 5: Stage 2 — News Research (42s - 58s)

**Visual:** News Research node expands. Most visually dynamic scene.

**Left side — 15 RSS feeds streaming in:**
Animate feed labels with small icons appearing in a stacked list:
```
MIT Technology Review
Wired
TechCrunch
The Verge
VentureBeat
Ars Technica
New York Times
Fast Company
Unite.ai
Daily AI
AI News
AI Weekly
AI Hub
Datamachina
Science Daily
```

Animated dots stream from each feed toward a central filter funnel.

**Center — 3-layer filter funnel:**

Layer 1: "Keyword Match" — dots enter, some pass (green), some filtered (red, fade). Label: "Must match trending topics"

Layer 2: "7-Day Dedup" — fewer dots, more filtered. Label: "Skip already-covered stories"

Layer 3: "Thematic Dedup" — final filter. Label: "One story per theme"

**Right side — 5 research file cards appear one by one:**
```
📄 pro-human-ai-declaration-resistance.md
   "90 leaders signed 5-principle AI governance declaration"
   Keyword Match: AI regulation fragmentation

📄 chatgpt-uninstalls-claude-rises-dod-deal.md
   "ChatGPT uninstalls spiked 295% in one day"
   Keyword Match: AI safety race / guardrails loosening

📄 cursor-2b-arr-ai-coding.md
   "Revenue doubled in 3 months to $2B ARR"
   Keyword Match: AI agents as enterprise infrastructure

📄 ai-therapy-chatbot-ethical-risks.md
   "15 ethical violations, zero regulatory mechanisms"
   Keyword Match: AI in healthcare / clinical LLMs

📄 enterprise-ai-operational-gap.md
   "76% in production, 66% have no one responsible"
   Keyword Match: AI agents as enterprise infrastructure
```

**Stat overlay (animate counter):** "87 feed items → 5 research files"

---

## Scene 6: Stage 3 — Brief Generation (58s - 75s)

**Visual:** Brief Writer node expands. Show transformation from raw research to structured brief.

**Left side — raw research card:**
```
📄 Research: pro-human-ai-declaration-resistance.md

Key Data Points:
• 90 political, religious, labor leaders
• Chatham House Rules secret meeting
• Steve Bannon + AFL-CIO signed same document
• Least popular principle: 94% approval
• General voter support: 69-80%
• 5 principles: human agency, power
  concentration, child protection,
  AI legal personhood, lethal weapons
```

**Center:** Animated transformation — data restructures, crystallizes with particle effects.

**Right side — the brief card builds section by section:**

```
📄 Brief: pro-human-ai-declaration-resistance.md
   status: draft

## HEADLINE
A cross-ideological coalition of 90+ leaders
has published a five-principle AI governance
declaration with 80%+ public support

## HOOK OPTIONS  ← (this section glows gold)

Provocative:
"Steve Bannon and the AFL-CIO just signed the
same AI governance document. Read the room."

Binary:
"AI governance written by tech companies:
voluntary, self-serving, stalled.
AI governance written by everyone else:
94% consensus, bipartisan, coming for legislation."

Contrarian:
"The most important AI policy document of 2026
was written in a hotel conference room —
and no tech company was allowed in the room."

## GREY AI ANGLE
## SUGGESTED FORMAT: carousel
## KEYWORDS + HASHTAGS
## RAW MATERIAL
```

**Then show 4 more brief cards fading in below, each showing their best hook:**

Card 2: `chatgpt-uninstalls-claude-rises-dod-deal.md`
Hook: "ChatGPT uninstalls: up 295%. Claude downloads: up 88%. Same weekend. Same news cycle."

Card 3: `cursor-2b-arr-ai-coding.md`
Hook: "Four years to $1 billion ARR. Three months to add the next billion. That's not growth — that's escape velocity."

Card 4: `ai-therapy-chatbot-ethical-risks.md`
Hook: "When a human therapist makes an ethical violation, there's a governing board. When an AI does it, there's nothing."

Card 5: `enterprise-ai-operational-gap.md`
Hook: "76% in production, 66% have no one responsible — that math ends badly."

**Callout:** "Briefs = structured ingredients, not finished posts"

---

## Scene 7: Stage 4 — Ranking (75s - 90s)

**Visual:** Ranker node expands. The scoreboard scene.

Show 5 brief cards arranged vertically. The 10-criterion scoring grid animates in beside them.

**Use these EXACT scores from the real pipeline output:**

```
                    Hook Data Angle Binary Emotion Carousel Timely Unique Audience Material TOTAL
pro-human-ai          2    2    2     2      2       2       2      2      2        2      20/20 ★
enterprise-ai-gap     2    2    2     2      2       2       1      1      2        2      18/20
ai-therapy-chatbot    2    1    2     2      2       2       1      2      2        2      18/20
llms-deanonymize      1    2    2     1      1       2       1      2      1        2      15/20
cursor-2b-arr         2    2    1     1      1       1       1      2      1        1      13/20
```

Animate scores filling in column by column (left to right). Each cell pops in. Totals calculate last.

The 20/20 row gets a gold glow. "WINNER" badge animates on.

**Then show the winner justification text fading in:**
"The Steve Bannon + AFL-CIO hook is the most scroll-stopping of any brief today — an unexpected ideological coalition creates instant curiosity — and the five governance principles map directly to a five-slide enterprise compliance checklist."

**Status animation:** `draft` → `winner` with a checkmark

**Text overlay:** "10 criteria. Brutally honest. One winner."

---

## Scene 8: Stage 5 — Compilation & Handoff (90s - 100s)

**Visual:** Compiler node expands. Final assembly.

Animate briefs (in rank order) and their paired research files sliding together:

```
📄 2026-03-04.md — Ready for Google Docs

Brief 1 — winner ★
(pro-human-ai-declaration-resistance)
[Brief content]
+ Source Research (The Verge article data)

Brief 2 — ranked
(enterprise-ai-operational-gap)
[Brief content]
+ Source Research

Brief 3 — ranked
(ai-therapy-chatbot-ethical-risks)
[Brief content]
+ Source Research

... 2 more
```

The compiled document slides into a Google Docs icon.

**Flow arrow:** "Human Review → Claude.ai LinkedIn Growth Engine → Publish"

---

## Scene 9: Architecture Reveal (100s - 112s)

**Visual:** Everything zooms out. Full pipeline visible at top. Below, show the "what powers this" breakdown.

Animate file tree:
```
📁 .claude/
  📁 agents/
    📄 seo-researcher.md       ← "Find trending keywords"
    📄 news-researcher.md      ← "Scrape & filter RSS feeds"
    📄 draft-writer.md         ← "Generate LinkedIn briefs"
    📄 post-ranker.md          ← "Score & pick winner"
    📄 content-compiler.md     ← "Compile for review"
  📁 commands/
    📄 generate-content.md     ← "Orchestrate all 5 agents"
📄 .mcp.json                   ← "Connect RSS + Google Trends"
📄 CLAUDE.md                   ← "Project instructions"
```

Next to the file tree, counters animate up:
```
Lines of code:          0
Markdown files:         8
JSON config:           14 lines
Custom infrastructure:  None
```

**Bold text fades in:** "The entire pipeline is markdown."

---

## Scene 10: Closing (112s - 120s)

**Visual:** Clean dark background. Text centered.

Line 1 (large, gold #D4A574): **"One command. Five agents. Zero code."**
Line 2 (medium, white): "Built with Claude Code"
Line 3 (small, muted #888): "grey.ai"

The `/generate-content` command types itself one more time at the bottom as a callback to Scene 2.

---

## Implementation Notes

**Component structure:**
```
src/
  compositions/
    ProductDemo.tsx           (main composition, sequences all scenes)
  scenes/
    ProblemScene.tsx
    OneCommandScene.tsx
    PipelineOverviewScene.tsx
    SEOKeywordsScene.tsx
    NewsResearchScene.tsx
    BriefGenerationScene.tsx
    RankingScene.tsx
    CompilationScene.tsx
    ArchitectureScene.tsx
    ClosingScene.tsx
  components/
    Terminal.tsx               (reusable CLI/terminal window)
    PipelineNode.tsx           (agent node in pipeline diagram)
    FileCard.tsx               (file card with content preview)
    FlowingParticles.tsx       (animated dots along connections)
    ScoreboardRow.tsx          (animated score cell filling)
    FilterFunnel.tsx           (3-layer funnel for Stage 2)
    TypewriterText.tsx         (character-by-character reveal)
    FadeIn.tsx                 (reusable spring-based fade+slide)
    HookCard.tsx               (brief card highlighting hook text)
  data/
    seoKeywords.ts             (real keyword data for Scene 4)
    researchFiles.ts           (real research summaries for Scene 5)
    briefs.ts                  (real brief data for Scene 6)
    scores.ts                  (real scoreboard data for Scene 7)
    hooks.ts                   (all real hook examples)
  styles/
    theme.ts                   (color palette, typography constants)
```

**Key Remotion APIs:**
- `useCurrentFrame()` and `interpolate()` for all animations
- `spring()` for natural motion (stiffness: 100, damping: 20)
- `<Sequence>` for scene timing
- `<AbsoluteFill>` for layered compositions
- `Easing.bezier()` for smooth transitions
- `measureSpring()` to calculate spring durations

**Frame math at 30fps:**
- Scene 1 (Problem): frames 0-360 (12s)
- Scene 2 (Command): frames 360-600 (8s)
- Scene 3 (Pipeline): frames 600-900 (10s)
- Scene 4 (SEO): frames 900-1260 (12s)
- Scene 5 (Research): frames 1260-1740 (16s)
- Scene 6 (Briefs): frames 1740-2250 (17s)
- Scene 7 (Ranking): frames 2250-2700 (15s)
- Scene 8 (Compile): frames 2700-3000 (10s)
- Scene 9 (Architecture): frames 3000-3360 (12s)
- Scene 10 (Closing): frames 3360-3600 (8s)

Total: 3600 frames = 120 seconds at 30fps

---

## All Real Hook Examples (for data files)

Use these verbatim — they are actual pipeline outputs:

**Winner (20/20):**
- Provocative: "Steve Bannon and the AFL-CIO just signed the same AI governance document. Read the room."
- Binary: "AI governance written by tech companies: voluntary, self-serving, stalled. AI governance written by everyone else: 94% consensus, bipartisan, and coming for legislation."
- Contrarian: "The most important AI policy document of 2026 was written in a hotel conference room — and no tech company was allowed in the room."

**Ranked (18/20) — enterprise-ai-operational-gap:**
- Stat Gap: "76% in production, 66% have no one responsible — that math ends badly."

**Ranked (18/20) — ai-therapy-chatbot-ethical-risks:**
- Provocative: "When a human therapist makes an ethical violation, there's a governing board. When an AI does it, there's nothing."
- Binary: "Human therapist breaks ethics: malpractice liability, governing board, remediation process. AI chatbot breaks ethics: no framework, no accountability, no mechanism."
- Contrarian: "The risk of AI therapy chatbots isn't that they'll give bad advice. It's that nobody is responsible when they do."

**Ranked (15/20) — chatgpt-uninstalls:**
- Stat Gap: "ChatGPT uninstalls: up 295%. Claude downloads: up 88%. Same weekend. Same news cycle."
- Provocative: "Safety guardrails didn't cost OpenAI the military contract. They cost it the App Store."

**Ranked (13/20) — cursor-2b-arr:**
- Stat Gap: "Four years to $1 billion ARR. Three months to add the next billion. That's not growth — that's escape velocity."
- Provocative: "$2 billion in revenue. Doubled in one quarter. The teams not using this are the experiment now."

---

## All Real SEO Keywords (for data files)

Use these verbatim:

**Trending Topics (12):**
1. Anthropic vs. Pentagon / Military AI Ethics
2. AI Safety Race / Guardrails Loosening
3. AI Agents as Enterprise Infrastructure
4. AI Agent Security Vulnerabilities
5. Small Open-Source Models Beating Proprietary
6. Context Engineering / Model Context Protocol
7. AI Regulation Fragmentation
8. LLMs as Primary Content Audience
9. AI in Healthcare / Clinical LLMs
10. OpenAI Dept of War Agreement
11. AI Lobbying vs. Safety Research Funding
12. Agentic AI in Finance

**High-Impact Phrases (10):**
1. "the race to the bottom on safety"
2. "agents are infrastructure now"
3. "small models, big implications"
4. "context engineering, not prompt engineering"
5. "your content's new audience is an LLM"
6. "safety as competitive advantage"
7. "the Balkanization of AI policy"
8. "prompt injection is the new SQL injection"
9. "from experimentation to execution"
10. "who watches the agents?"

**Hashtags (15 with follower counts):**
1. #AI (6M+)
2. #ArtificialIntelligence
3. #AIAgents (trending)
4. #AISafety (surging)
5. #GenerativeAI
6. #FutureOfWork (1M+)
7. #CyberSecurity (1.5M+)
8. #OpenSource
9. #Technology (15M+)
10. #Innovation (18M+)
11. #MachineLearning
12. #Leadership (25M+)
13. #DataPrivacy
14. #EnterpriseAI
15. #PromptEngineering

---

## Real Scoreboard Data (for Scene 7)

```typescript
const scores = [
  {
    rank: 1,
    file: "pro-human-ai-declaration-resistance",
    scores: { hook: 2, data: 2, angle: 2, binary: 2, emotion: 2, carousel: 2, timely: 2, unique: 2, audience: 2, material: 2 },
    total: 20,
    status: "winner",
    headline: "90+ cross-ideological leaders publish 5-principle AI governance declaration",
    bestHook: "Steve Bannon and the AFL-CIO just signed the same AI governance document. Read the room.",
    why: "The Steve Bannon + AFL-CIO hook is the most scroll-stopping — an unexpected ideological coalition creates instant curiosity — and the five principles map to a five-slide enterprise compliance checklist."
  },
  {
    rank: 2,
    file: "enterprise-ai-operational-gap",
    scores: { hook: 2, data: 2, angle: 2, binary: 2, emotion: 2, carousel: 2, timely: 1, unique: 1, audience: 2, material: 2 },
    total: 18,
    status: "ranked",
    headline: "76% of enterprises running AI in production — 66% have no one responsible for it",
    bestHook: "76% in production, 66% have no one responsible — that math ends badly."
  },
  {
    rank: 3,
    file: "ai-therapy-chatbot-ethical-risks",
    scores: { hook: 2, data: 1, angle: 2, binary: 2, emotion: 2, carousel: 2, timely: 1, unique: 2, audience: 2, material: 2 },
    total: 18,
    status: "ranked",
    headline: "15 ethical violations in AI therapy chatbots — zero regulatory mechanisms",
    bestHook: "When a human therapist makes an ethical violation, there's a governing board. When an AI does it, there's nothing."
  },
  {
    rank: 4,
    file: "llms-deanonymize-pseudonymous-users",
    scores: { hook: 1, data: 2, angle: 2, binary: 1, emotion: 1, carousel: 2, timely: 1, unique: 2, audience: 1, material: 2 },
    total: 15,
    status: "ranked",
    headline: "LLMs can deanonymize pseudonymous users with 90% precision from free text alone",
    bestHook: "Your pseudonym isn't protecting you. LLMs just proved it — 90% accuracy, free text only."
  },
  {
    rank: 5,
    file: "cursor-2b-arr-ai-coding",
    scores: { hook: 2, data: 2, angle: 1, binary: 1, emotion: 1, carousel: 1, timely: 1, unique: 2, audience: 1, material: 1 },
    total: 13,
    status: "ranked",
    headline: "AI coding tool hits $2B ARR — doubled in one quarter",
    bestHook: "Four years to $1 billion ARR. Three months to add the next billion. That's not growth — that's escape velocity."
  }
];
```

---

## Real RSS Feed List (for Scene 5)

```typescript
const rssFeeds = [
  { name: "MIT Technology Review", url: "technologyreview.com" },
  { name: "Wired", url: "wired.com" },
  { name: "TechCrunch", url: "techcrunch.com" },
  { name: "The Verge", url: "theverge.com" },
  { name: "VentureBeat", url: "venturebeat.com" },
  { name: "Ars Technica", url: "arstechnica.com" },
  { name: "New York Times", url: "nytimes.com" },
  { name: "Fast Company", url: "fastcompany.com" },
  { name: "Unite.ai", url: "unite.ai" },
  { name: "Daily AI", url: "dailyai.com" },
  { name: "AI News", url: "artificialintelligence-news.com" },
  { name: "AI Weekly", url: "aiweekly.co" },
  { name: "AI Hub", url: "aihub.org" },
  { name: "Datamachina", url: "datamachina.substack.com" },
  { name: "Science Daily", url: "sciencedaily.com" }
];
```

---

## Real Research File Example (for Scene 6 transformation)

This is the full winning research file that transforms into the winning brief:

```
Title: Inside the Secret Meeting That Led to the AI Political Resistance
Source URL: theverge.com
Publication Date: March 4, 2026
Keyword Match: AI regulation fragmentation, AI safety race, AI lobbying vs. safety research funding

Summary:
In early January 2026, approximately 90 political, religious, labor, and community leaders
gathered in a New Orleans Marriott for a secret conference organized by the Future of Life
Institute (FLI). The meeting was deliberately kept free of tech industry representatives.
On March 4, FLI published the result: the "Pro-Human AI Declaration," a five-principle
document centered on keeping AI development human-centered, preventing concentration of
power, protecting children and families, and preserving human agency.

Key Data Points:
- Organized by Max Tegmark, MIT professor (TIME 100 AI list)
- ~90 attendees from across political spectrum; Chatham House Rules
- Signatories: AFL-CIO, Screen Writers Guild, SAG-AFTRA, Congress of Christian Leaders
- Individual signatories: Ralph Nader to Steve Bannon
- Least popular principle still received 94% approval from attendees
- General voter polling: worst-performing principle at 69% support
- 5 principles: human agency, power concentration, child/family protection,
  AI legal personhood, autonomous lethal weapons
- No tech company representatives invited — deliberate design choice
- Contrast: 2017 Asilomar AI Principles signed by Altman, Musk, Hassabis —
  the same people the 2026 declaration implicitly opposes

Why It Matters:
When labor unions, religious organizations, and conservative think tanks align on AI
guardrail principles, legislation follows. Organizations should treat this declaration
as a preview of future regulatory requirements, not a fringe political statement.
```

---

## Real Brief File Example (the winner — for Scene 6 output)

```yaml
---
source_file: content/research/2026-03-04-pro-human-ai-declaration-resistance.md
keywords_file: content/seo/2026-03-04-keywords.md
status: winner
created_date: 2026-03-04
---
```

```
## HEADLINE
A cross-ideological coalition of 90+ labor, religious, and civic leaders — deliberately
excluding all tech company representatives — has published a five-principle AI governance
declaration with 80%+ public support on every clause.

## KEY FACTS
- Least popular principle: 94% approval from attendees; 69% from general voters
- Signatories span Ralph Nader to Steve Bannon — first cross-ideological AI alignment
- 5 principles target enterprise-relevant compliance risk areas
- Source credibility: Future of Life Institute, Chatham House Rules, Tavern Research poll

## GREY AI ANGLE
When labor unions, conservative think tanks, and religious organizations sign the same
governance document, that is not a fringe political signal — it is the leading indicator
of bipartisan legislation. Organizations need to audit their AI deployments against these
five principles now.

## HOOK OPTIONS
Provocative: "Steve Bannon and the AFL-CIO just signed the same AI governance document.
Read the room."

Binary: "AI governance written by tech companies: voluntary, self-serving, stalled.
AI governance written by everyone else: 94% consensus, bipartisan, and coming for
legislation."

Contrarian: "The most important AI policy document of 2026 was written in a hotel
conference room — and no tech company was allowed in the room."

## SUGGESTED FORMAT
carousel
Reasoning: Five principles map to five carousel slides with enterprise-readiness implications.

## KEYWORDS
- Trending topics: AI regulation fragmentation; AI lobbying vs. safety research funding
- Hashtags: #AISafety #AIGovernance #Leadership #ArtificialIntelligence #FutureOfWork

## RAW MATERIAL
Max Tegmark: "If the government won't do it, then the people have to force the government
to do it." 2017 Asilomar Principles signed by Altman, Musk, Hassabis — the same people
the 2026 declaration implicitly opposes. FLI running "Protect What's Human" voter education
campaign ahead of 2026 midterms. No tech company representatives invited — deliberate
design choice.
```


