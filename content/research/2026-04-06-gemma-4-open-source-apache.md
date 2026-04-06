---
title: "Google Announces Gemma 4 Open AI Models, Switches to Apache 2.0 License"
source_url: "https://arstechnica.com/ai/2026/04/google-announces-gemma-4-open-ai-models-switches-to-apache-2-0-license/"
publication_date: "2026-04-02"
keyword_match: ["open source AI models", "agentic AI", "vibe coding and AI-assisted development"]
---

# Google Announces Gemma 4 Open AI Models, Switches to Apache 2.0 License

**Title:** Google Announces Gemma 4 Open AI Models, Switches to Apache 2.0 License

**Source URL:** https://arstechnica.com/ai/2026/04/google-announces-gemma-4-open-ai-models-switches-to-apache-2-0-license/

**Publication Date:** April 2, 2026

**Keyword Match:** open source AI models, agentic AI, vibe coding and AI-assisted development

## Summary

Google has launched Gemma 4, a new family of four open-weight AI models optimized for local deployment, and simultaneously dropped its restrictive custom license in favor of Apache 2.0 — a move developers have been demanding since the Gemma line launched. The four models span from mobile-optimized edge variants (Effective 2B and 4B, designed for smartphones and single-board computers) to high-performance local server models (26B Mixture of Experts and 31B Dense). Google claims Gemma 4's 31B variant will debut at number three on the open-source Arena leaderboard, despite being a fraction of the size of the top two models. The Apache 2.0 switch is potentially the more consequential announcement — it eliminates the legal uncertainty that had caused many developers and enterprises to avoid building on Gemma despite its strong technical performance.

## Key Data Points

- **Four model sizes**: Effective 2B (E2B) and 4B (E4B) for mobile/edge, 26B Mixture of Experts and 31B Dense for local servers
- **26B MoE model** activates only **3.8 billion parameters** during inference — high tokens-per-second at much lower compute cost
- **Context window**: 128k tokens for edge models, **256k tokens** for 26B and 31B
- **128k/256k token context windows** on local hardware vs. 1 million tokens for cloud-based Gemini
- Gemma 31B projected to rank **#3 on the Arena open-source leaderboard**, behind GLM-5 and Kimi 2.5
- Works across **140+ languages**
- Previous Gemma license allowed Google to unilaterally update prohibited-use policies; **Apache 2.0** has no commercial restrictions and cannot be modified retroactively
- Native support for **function calling, structured JSON output, and agentic tool APIs** — purpose-built for agent workflows
- Gemini Nano 4 (the next on-device AI for Pixel phones) will be based on Gemma 4 E2B and E4B

## Why It Matters

The Gemma 4 release matters on two levels. Technically, it puts genuinely competitive open-weight models within reach of organizations that need to run AI locally — whether for privacy, latency, cost, or regulatory reasons. Strategically, the Apache 2.0 licensing switch removes the single biggest adoption barrier for enterprises and developers who had been building on Meta's Llama models instead. The timing is significant: with open-source AI governance becoming a boardroom concern, Google is signaling that "open" and "trustworthy" can coexist. For technical audiences on LinkedIn, this is the story that changes which model stack they recommend to their teams.

## Related Themes

Open source AI, Google Gemma, Apache 2.0, local AI deployment, agentic AI, AI infrastructure, enterprise AI, edge AI, mobile AI, developer tools
