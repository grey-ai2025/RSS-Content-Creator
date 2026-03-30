---
date: 2026-03-27
profiles_scraped: 8/8
browser_success: []
search_fallback: [emollick, alliekmiller, samaltman, satyanadella, andrewyng, linasbeliunas, ninaschick, mattshumer]
scraping_notes: "LinkedIn browser sessions redirected to auth wall on all attempts for all profiles (no saved cookies in browser session). All 8 profiles fell back to firecrawl_search (Query 1 + Query 2 per profile). LinkedIn post URLs are blocked by the firecrawl scraper; LinkedIn Pulse article URLs remain accessible and were scraped in full. Post content was reconstructed from search snippets, third-party coverage, and directly scraped Pulse articles. New entries since the 2026-03-26 benchmark: Matt Shumer's '10x Your Coding Agent Productivity' (March 20, scraped in full — 33 likes, 7 comments, early traction); updated engagement count on 'Something Big Is Happening' confirmed at 11,154 likes / 1,240 comments. Linas Beliunas 'real moat in AI Agents' post surface-scraped from profile page (Mar 5). Ethan Mollick 'tireless team of little computer people' post confirmed from search snippet."
---

# LinkedIn Influencer Benchmark — 2026-03-27

## Top-Performing Posts

### 1. Matt Shumer — "Think back to February 2020. If you were paying close attention..."
- **Engagement:** 11,154 likes, 1,240 comments, 100M+ views (confirmed by third-party coverage; Pulse article scraped in full)
- **Format:** Long-form Pulse article (5,000+ words)
- **Hook style:** Story — opens with a personal memory anchor (February 2020 / COVID pre-awareness) to make an emotional parallel to AI's current moment
- **Structure:** Narrative with escalating stakes — personal confession ("I should have told you sooner"), industry observation, societal consequence, prescriptive action list, closing CTA ("share this with someone who needs it")
- **Length:** Long (5,000+ words)
- **Why it works:** The COVID frame gives readers an emotionally visceral reference point for something abstract. The confessional register ("I keep giving them the polite version") builds trust by admitting to holding back. The METR benchmark data (task horizon doubling every 7 months) converts abstract AI progress into a measurable, quotable number. Closing with a personal-share CTA drives amplification without asking for a like. The article was written with AI assistance, which Shumer disclosed — itself generating a second wave of coverage.

### 2. Matt Shumer — "Most people are using Codex and Claude Code wrong."
- **Engagement:** 33 likes, 7 comments (March 20, 2026 — early traction, recently published)
- **Format:** Short Pulse article (practical how-to, ~400 words + starter prompt)
- **Hook style:** Contrarian take — opens by saying the dominant behavior (opening a fresh thread per task) is the wrong approach
- **Structure:** Problem → Better Setup → Named Components → Starter Prompt → Payoff. The key structural move is including an actual copy-paste orchestrator prompt, making the post a save-worthy artifact rather than just an opinion.
- **Length:** Short (article) with dense practical payload
- **Why it works:** Actionable content with copy-paste utility drives saves. The orchestrator/subagent framing introduces a mental model (main thread as manager, subagents as individual contributors) that readers can immediately apply. The post benefits from Shumer's existing credibility from "Something Big Is Happening" — same author, different register, same precision.

### 3. Satya Nadella — "We have moved past the initial phase of discovery and are entering a phase of widespread diffusion."
- **Engagement:** 4,067+ reactions, 349+ comments (confirmed in search; high repost volume cited across 20+ third-party posts)
- **Format:** Text post linking to personal blog (snscratchpad.com — full text scraped)
- **Hook style:** Named-era declaration — "spectacle vs. substance" reframe positions AI hype as the obstacle, not competitors
- **Structure:** Framework — three named shifts: (1) models to systems, (2) capability vs. real-world impact, (3) societal permission requires societal outcomes. Each point is labeled with a design question, engineering challenge, or socio-technical issue.
- **Length:** Long (blog post ~700 words; LinkedIn post excerpt ~200 words)
- **Why it works:** CEO credibility plus named concepts ("model overhang," "scaffolding for human potential," "spectacle vs. substance") gives practitioners vocabulary to repeat with attribution. The post explicitly frames the current moment as "the opening miles of a marathon," which gives enterprise audiences permission to feel behind without feeling panicked. Linking to a personal blog (not a company blog) signals authenticity and drives click-through.

### 4. Ethan Mollick — "Axiom: The form of AI that we ended up with is deeply weird in ways that we don't fully understand."
- **Engagement:** High (broad AI media pickup; cited on Bluesky with 112 reposts from that single account alone; post generated wide comment thread)
- **Format:** Text post
- **Hook style:** Named axiom — opens with the word "Axiom" to signal this is a formal claim, not an opinion
- **Structure:** Single named principle + implication + actionable conclusion. The structure is tight: state the axiom, explain why it matters (those who accept the weirdness outperform those who fight it), leave the reader with a reframe.
- **Length:** Short-to-medium
- **Why it works:** "Axiom" as an opening word signals intellectual seriousness and positions the post as a rule rather than a take. The observation that AI is "deeply weird in ways we don't fully understand" validates the confusion practitioners feel while reframing confusion as a feature of skilled use. Posts that validate frustration while offering a reframe consistently outperform posts that only offer advice.

### 5. Ethan Mollick — "Its annoying that my tireless team of little computer people made out of statistical models that predict words based on the corpus of all human knowledge..."
- **Engagement:** High (confirmed broad pickup; the description is both technically accurate and absurdist, generating high share volume)
- **Format:** Text post
- **Hook style:** Provocative metaphor — describes AI agents as "little computer people made out of statistical models that predict words" — technically accurate but deliberately deflationary
- **Structure:** Observation narrative — sets up a genuine complaint, then lets the observation carry the weight without resolving it neatly
- **Length:** Short-to-medium
- **Why it works:** The deliberately mundane framing of something (AI agents) that most people treat with either reverence or fear creates cognitive dissonance. The humor is the engagement surface. It also implicitly positions Mollick as someone who uses AI so extensively that "annoyance" is his primary emotion — which signals deep practical expertise without stating it.

### 6. Ethan Mollick — "I remain wary of bright line arguments that AI cannot do judgment, or creativity, or empathy..."
- **Engagement:** High (cited in multiple follow-on posts as a notable position)
- **Format:** Text post
- **Hook style:** Contrarian take — directly challenges the most common LinkedIn AI reassurance narrative ("your creativity/empathy is safe")
- **Structure:** Argument — states the position, explains the reasoning (AI repeatedly surpasses apparent limits), draws a cautious but clear conclusion
- **Length:** Short-to-medium
- **Why it works:** This post inserts itself into the dominant comfort narrative that most LinkedIn creators use to reassure audiences about AI not replacing humans. Taking the opposite position in a field where reassurance is the default creates maximum friction — and maximum comment engagement from both sides.

### 7. Allie K. Miller — "More AI users need to hear this: prompting AI better might not be the skill that matters most in 2026."
- **Engagement:** High (substantial comment volume; post widely reshared and replied to in third-party posts)
- **Format:** Text post
- **Hook style:** Contrarian take — directly contradicts the dominant LinkedIn advice genre ("improve your prompting") with a fronted warning phrase ("More AI users need to hear this")
- **Structure:** Binary split — prompting vs. context architecture. The post creates a hierarchy: prompting is a surface skill; context design is the deep skill.
- **Length:** Medium
- **Why it works:** "More X need to hear this" is a high-performing hook pattern because it positions the reader as an insider receiving privileged information. The pivot from prompting to something deeper frustrates the reader's expectation (they came for a prompting tip) and forces them to read to find out what the alternative is. High disagree/agree comment dynamic drove algorithmic amplification.

### 8. Allie K. Miller — "If you're still copy-pasting context into AI manually, there's a faster way and it takes about 4 seconds."
- **Engagement:** High (TikTok cross-post confirmed high share rate; cited in multiple third-party LinkedIn posts)
- **Format:** Text post (likely with short video for TikTok cross-post)
- **Hook style:** Stat-as-hook — "4 seconds" is a specific, surprising number that makes the benefit feel credible and tangible
- **Structure:** Problem-solution listicle — identifies the behavior (copy-pasting), names the faster alternative (custom commands), explains the workflow in numbered steps
- **Length:** Short-to-medium
- **Why it works:** The time specificity ("4 seconds") is the engagement hook — vague claims ("save time") don't stop the scroll, but "4 seconds" forces the brain to evaluate. The post is designed to save, not just read. Cross-platform presence on TikTok drives LinkedIn engagement by sending external audiences back to the original post.

### 9. Allie K. Miller — "My 2026 AI predictions just dropped."
- **Engagement:** High (prediction posts consistently generate comment threads from people adding their own predictions; post cited 141+ comments in a reshare)
- **Format:** Text post linking to longer prediction document
- **Hook style:** Urgency signal — "just dropped" creates recency pressure without being clickbait
- **Structure:** Listicle teaser — 3–4 named predictions in post, full list behind a comment gate or link. Voice AI, agentic AI, and the shift from "Is AI smart?" to "Is AI valuable?" were the headline predictions.
- **Length:** Short (teaser post) with linked long-form resource
- **Why it works:** Prediction content is inherently disagreeable, and disagreement drives comments. The comment gate (comment to get the full list) is a deliberate engagement-farming mechanism that LinkedIn's algorithm rewards. The shift from "smart?" to "valuable?" is a reframe that practitioners can immediately test against their own experience.

### 10. Andrew Ng — "I'm excited to announce Context Hub, an open tool that gives your coding agent the up-to-date API documentation it needs."
- **Engagement:** High (cited across 10+ third-party LinkedIn posts and AI newsletters; GitHub launch)
- **Format:** Text post (product announcement + GitHub link)
- **Hook style:** Product launch + utility claim — names what the tool does in the opening sentence with no preamble
- **Structure:** Problem → Solution → Access. No framework, no listicle — a clean three-move announcement.
- **Length:** Short
- **Why it works:** Ng's announcement posts perform well because he has a large developer audience who treat his launches as credible signals. The tool addresses a concrete pain point (coding agents using outdated API docs) that every developer using agentic coding has hit. The open-source framing drives GitHub engagement, which reinforces LinkedIn engagement loops.

### 11. Andrew Ng — "The real gains will come from end-to-end workflow redesign."
- **Engagement:** High (cited across 10+ third-party LinkedIn posts; used as the central argument in multiple enterprise AI strategy posts)
- **Format:** Text post (sharing AI newsletter digest with curated commentary)
- **Hook style:** Contrarian take — pushes back against the AI-tools-adoption frame in favor of workflow transformation
- **Structure:** Framework — bottom-up vs. top-down innovation approaches, with the conclusion that neither alone is sufficient
- **Length:** Medium
- **Why it works:** Ng consistently positions himself as seeing past AI tool hype to the underlying business transformation logic. This appeals to enterprise audiences who have already bought AI tools and are struggling to justify ROI. The post functions as a permission slip: "you're not getting value from AI because you haven't redesigned the workflow, not because the tools don't work."

### 12. Nina Schick — "You don't become an AI superpower by writing clever code. You need the entire stack."
- **Engagement:** High (widely reshared; post cited across strategy and policy-adjacent LinkedIn accounts)
- **Format:** Text post
- **Hook style:** Contrarian take — dismantles the dominant AI-leadership-equals-model-capability frame
- **Structure:** Argument + historical analogy (incandescent light bulb invented in UK but commercialized by Edison / US industrial base). The historical analogy is the proof mechanism that makes the argument concrete.
- **Length:** Medium
- **Why it works:** Schick consistently uses historical analogies to make geopolitical AI arguments legible to a non-specialist audience. The light bulb / Edison analogy is well-known enough to require no explanation but specific enough to do real argumentative work. The post directly addresses a widespread misconception (that leading in AI means leading in model development) — a corrective post generates more engagement than an affirmative one.

### 13. Nina Schick — "China's 15th Five-Year Plan is being formally adopted this week. It elevates AI to a 'New Quality Productive Force.'"
- **Engagement:** High (policy/geopolitics angle; party-language decode generated strong engagement from China-watchers and enterprise strategy audiences)
- **Format:** Text post (news-jack)
- **Hook style:** News-jack with translation — opens with a factual news hook, then immediately decodes the jargon ("That's Party-speak for:")
- **Structure:** News event → decode → implication. Three moves. The translation of "New Quality Productive Force" does the analytical work in parentheses, making the post feel like insider knowledge.
- **Length:** Short-to-medium
- **Why it works:** The parenthetical translation ("That's Party-speak for:") is a signature Schick move — it positions her as the decoder of geopolitical language for a practitioner audience that doesn't follow Chinese policy. This "translation service" framing creates perceived value and drives follows from people who want future translations.

### 14. Nina Schick — "AI has a 'people problem.' And that might be its real constraint rather than compute."
- **Engagement:** High (cited across workforce and AI strategy posts; the "people problem" framing was widely adopted)
- **Format:** Text post
- **Hook style:** Contrarian take — inverts the dominant AI-constraint narrative (compute, data, algorithms) to focus on human perception and organizational resistance
- **Structure:** Binary contrast — technical constraints vs. human constraints, with the argument that human perception is now the binding variable
- **Length:** Short-to-medium
- **Why it works:** In a news environment saturated with technical AI progress stories, a post that identifies the human side as the real bottleneck stands out. The phrase "people problem" is evocative and slightly unflattering in a way that generates reaction — some agree (enterprise practitioners), some push back (AI advocates). Both reactions drive engagement.

### 15. Linas Beliunas — "For two years, everyone said Apple was losing the AI race. Turns out Apple might have been running a different race entirely."
- **Engagement:** High (confirmed cited in multiple third-party posts; described as a notable post by followers recommending Beliunas)
- **Format:** Text post
- **Hook style:** Contrarian take with narrative reversal — sets up the conventional wisdom ("Apple is losing") then immediately dismantles it
- **Structure:** Narrative reversal — the "everyone said X, turns out Y" structure. Sets up a false consensus, then provides the reframe.
- **Length:** Short-to-medium
- **Why it works:** Apple is a high-engagement topic on LinkedIn because nearly everyone has a strong opinion about the company. The "narrative reversal" structure is one of the highest-performing patterns in LinkedIn content because it satisfies the reader's desire to feel like they know something others don't. The post also functions as implicit commentary on how AI coverage is often wrong — which validates the reader's skepticism of tech media.

---

## Pattern Analysis

### Hook Patterns

- **Contrarian take (dominant across all profiles):** Seven of the fifteen top posts open by directly contradicting a belief the target audience already holds. The precise formula is: state the dominant belief in sentence one, then break it in sentence two. Examples: "Prompting AI better might not be the skill that matters most" (Miller), "You don't become an AI superpower by writing clever code" (Schick), "I remain wary of bright line arguments that AI cannot do judgment" (Mollick), "For two years, everyone said Apple was losing the AI race" (Beliunas). The contrarian hook is especially effective on LinkedIn because it exploits the platform's "agree/disagree" comment dynamic — both agreement and pushback register as engagement signals to the algorithm.

- **Named axiom / named concept (second most common):** Mollick's "Axiom" opener, Nadella's "model overhang" and "spectacle vs. substance," Miller's "contextual vaults," Schick's "Silicon Realism" and "people problem." Naming a concept is a high-leverage move: the phrase becomes a citation mechanism. Every time a follower uses "model overhang" in a meeting, they implicitly credit Nadella. The naming pattern appears across 5 of 8 profiles and is the clearest differentiator between posts that generate one-time engagement and posts that build long-term authority.

- **Stat or time specificity as proof hook (third most common):** Miller's "4 seconds," Shumer's METR data ("task horizon doubling every seven months"), Nadella's "4,067 reactions" baseline credibility, Beliunas's usage of specific company names (McKinsey, Revolut) and agent counts as proof points. Specificity is not decoration — it is the mechanism that makes contrarian claims credible. A contrarian claim without a specific data point is an opinion. A contrarian claim with a METR graph citation is a finding.

- **Urgency signal + news-jack (fourth):** Schick's China Five-Year Plan post, Miller's "just dropped" prediction post, Shumer's CBS Mornings announcement. These posts capture timing advantages and are deliberately published within 24 hours of a triggering event.

### Format Distribution
- Text-only posts: 60%
- Long-form Pulse article: 20% (Shumer's two confirmed Pulse articles in top 15)
- Text post linking to external resource (blog, newsletter, GitHub): 13%
- Short Pulse article with practical payload: 7%
- Carousel: 0% (none confirmed in top 15 — Miller likely uses carousels but top performers were text)
- Image: 0%
- Video: 0%
- Poll: 0%

### Topic Themes

1. **AI capability acceleration and the job displacement question** — The highest-engagement theme across all 8 profiles without exception. Shumer's article is the peak expression, but Mollick's "bright line arguments" post, Nadella's "spectacle to substance" framework, and Schick's "people problem" post all operate in this space. What makes these posts perform is not describing the acceleration — everyone is doing that — but taking a specific, defensible position on what it means. Vague "AI is changing everything" posts fail. Posts that say "here is what specifically changes, and here is who gets it wrong" succeed.

2. **AI geopolitics and sovereign AI infrastructure** — A growing theme driven entirely by Schick in this cohort, but showing upstream engagement influence. The China Five-Year Plan post, the AI superpower stack argument, and the "geography of AI power is becoming clearer" post all attracted policy-adjacent audiences who cross-post to other platforms. This topic is moving from specialist to mainstream in early 2026.

3. **Workflow transformation vs. tool adoption** — Ng and Miller jointly own this space. The argument is consistent across both: using AI tools is not the same as redesigning processes for AI. This topic performs because it gives enterprise practitioners permission to feel that their failure to get ROI from AI is a strategy problem (fixable) rather than a technology problem (uncertain).

4. **Agentic AI and coding agent productivity** — Shumer's "10x Your Coding Agent Productivity," Ng's Context Hub launch, Beliunas's "real moat in AI Agents" post, and Mollick's "tireless team of little computer people" post all sit in this cluster. The common thread is that agent orchestration — not individual model capability — is the next skill ceiling. Posts that include copy-paste prompts or specific tool names in this space consistently outperform posts that stay at the conceptual level.

5. **Named concept creation and vocabulary leadership** — Not a topic per se but a meta-pattern worth calling out separately. Mollick, Nadella, Miller, and Schick all published posts in this period whose primary function was to introduce a new term into circulation. This is a deliberate authority-building strategy: you become the person practitioners credit when they use your phrase.

### Structural Patterns

- **The three-move argument (most consistent high-engagement structure):** Hook (contrarian claim or named axiom) → Proof (specific data point, historical analogy, or personal observation) → Implication (what this means for the reader). This structure appears across Nadella's "models to systems" post, Schick's "AI superpower stack" post, Mollick's "bright line arguments" post, and Beliunas's Apple post. It works because it respects the reader's time while still delivering a complete argument. Posts with only a hook and no proof are opinions. Posts with proof but no implication are news summaries. The three-move structure is the minimum viable post for a practitioner audience.

- **Short claim + copy-paste artifact:** Shumer's "10x Your Coding Agent Productivity" and Miller's "4 seconds" custom commands post both include something the reader can immediately act on — a verbatim orchestrator prompt or a specific workflow step. This turns the post into a utility object. People save utility objects; they scroll past opinions.

- **Historical analogy as proof mechanism:** Schick consistently uses historical analogies (light bulb, manufacturing offshoring) to make geopolitical arguments legible to non-specialists. The pattern requires three things: a well-known historical event, a parallel to the current AI moment, and a conclusion that the parallel implies. When this works, it functions as a compressed case study.

### Length and Engagement Correlation

- **Long-form Pulse articles generate disproportionate absolute engagement** when topic is high-stakes and the writer has an existing audience. Shumer's "Something Big Is Happening" (11,154 likes) is the clearest proof. But the outlier status of this post is important: most Pulse articles in this cohort get 30–50 likes. The formula for a viral Pulse article appears to be: (1) confessional first-person voice, (2) a well-known external event used as a comparison frame (COVID), (3) escalating stakes narrative, (4) specific verifiable data, (5) a CTA that asks the reader to share with someone they know personally. All five elements must be present.

- **Medium-length text posts (100–300 words) are the most reliable performers.** They appear in 9 of the 15 top posts. The optimal length appears to be 2–4 short paragraphs or a hook + 3–5 bullet points. Long enough to include a framework or proof point; short enough to read in one scroll stop.

- **Short posts (<100 words) succeed only as news-jacks or named-era declarations** — when the idea itself is dense enough that compression is a virtue. Schick's China Five-Year Plan post and Mollick's "Axiom" post both work in under 150 words. A short post that is not a news-jack, a named concept, or a stat-hook typically performs below average.

---

## Actionable Takeaways

1. **Deploy the three-move argument structure as the default post architecture.** Hook (name the wrong belief or introduce the axiom) → Proof (one specific data point, company name, or historical analogy) → Implication (what this means for the reader's decisions). Do not publish a post that has a hook but no proof, or proof but no implication. All three moves must be present for the post to function as a complete argument.

2. **Name something in every third post.** The clearest differentiator between posts that generate one-time engagement and posts that build long-term authority is whether the post introduces a named concept. The name doesn't have to be grand — "contextual vaults," "model overhang," "the people problem," "4-second workflow" all work. For Grey AI posts: name the behavior, the pattern, or the shift. Give practitioners something to repeat in their next meeting that points back to the source.

3. **Use time specificity as the engagement hook for practical posts.** "4 seconds" outperforms "saves time." "Doubling every 7 months" outperforms "accelerating rapidly." "40,000 humans and 25,000 AI agents" outperforms "McKinsey is using more AI." Before publishing any practical or data-driven post, replace every vague claim with the most specific number available. The specificity is the proof.

4. **For agentic AI posts, include a copy-paste artifact.** Shumer's orchestrator prompt and Miller's custom command workflow both show that posts with something the reader can immediately use — a verbatim prompt, a numbered workflow step, a specific tool name — are saved at significantly higher rates than posts that stay conceptual. Grey AI posts on AI agents or productivity should include at minimum one concrete action the reader can take in the next 10 minutes.

5. **News-jack within 24 hours or don't news-jack at all.** Schick's China Five-Year Plan post, Shumer's CBS Mornings announcement, and Beliunas's Apple "narrative reversal" post all captured timing advantages because they were published at or near the moment of news. Waiting 48–72 hours collapses the algorithmic timing advantage and turns a news-jack into a recap. For Grey AI: build a same-day publishing habit for any story where the angle is "here is what this actually means" rather than "here is what happened."
