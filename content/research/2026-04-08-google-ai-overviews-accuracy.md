---
date: 2026-04-08
---

# Google AI Overviews Is Wrong 10% of the Time — Generating Millions of Errors Daily

**Title:** Testing suggests Google's AI Overviews tell millions of lies per hour

**Source URL:** https://arstechnica.com/google/2026/04/analysis-finds-google-ai-overviews-is-wrong-10-percent-of-the-time/

**Publication Date:** April 7, 2026

**Keyword Match:** AI reliability and hallucination risk (#4)

**Summary:**
A new analysis by The New York Times — conducted with AI startup Oumi using the SimpleQA evaluation benchmark — found that Google's AI Overviews answers search queries incorrectly approximately 10% of the time. Given the scale of Google's search traffic, that error rate translates to tens of millions of wrong answers delivered every day, or hundreds of thousands per minute. The accuracy improved from 85% under Gemini 2.5 to 91% under Gemini 3, but Oumi's testing showed the remaining error rate is still enormous at Google's scale. Google disputes the methodology, arguing SimpleQA contains some incorrect reference answers and that the test doesn't reflect real-world search patterns. The core problem exposed is structural: Google routes most queries to faster, cheaper Gemini Flash models rather than its best Gemini Pro model, trading accuracy for speed and cost.

**Key Data Points:**
- AI Overviews accuracy: 91% under Gemini 3 (up from 85% under Gemini 2.5), per Oumi's SimpleQA benchmark testing
- The 9% error rate at Google's scale means hundreds of thousands of incorrect AI answers per minute
- Google uses Gemini Flash models "most of the time" for AI Overviews — not its most capable Gemini Pro model
- Without grounding (web search), Google's own benchmarks for Gemini models show 60–70% factual accuracy
- Google's response: "This study has serious holes. It doesn't reflect what people are actually searching on Google"
- Google itself reminds users: "AI can make mistakes, so double-check responses"
- Example errors: AI Overviews cited a source for a date it got wrong, and denied the existence of a Classical Music Hall of Fame while citing its own website

**Why It Matters:**
For any professional whose team or workflow relies on Google search results surfaced through AI Overviews — researchers, marketers, analysts, support staff, product managers — this story draws a sharp line between AI-generated convenience and verified accuracy. It also matters for enterprise buyers evaluating AI tools for customer-facing or compliance-sensitive use cases: a 10% error rate that presents wrong answers with full confidence is a different risk profile than a tool that flags uncertainty. This is a concrete data point for the broader hallucination risk conversation that any leader making AI adoption decisions needs to understand.

**Related Themes:** AI reliability, hallucination, Google, Gemini, enterprise AI risk, AI accuracy, search AI, generative AI
