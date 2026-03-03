---
date: 2026-03-04
---

# LLMs Can Unmask Pseudonymous Users at Scale With Surprising Accuracy

**Title:** LLMs can unmask pseudonymous users at scale with surprising accuracy

**Source URL:** https://arstechnica.com/security/2026/03/llms-can-unmask-pseudonymous-users-at-scale-with-surprising-accuracy/

**Publication Date:** March 3, 2026

**Keyword Match:** AI agent security vulnerabilities (Keyword 4); AI regulation fragmentation / data privacy (Keyword 7)

**Summary:**
New peer-reviewed research published on arXiv reveals that large language models can identify the real identities behind pseudonymous social media accounts with far greater accuracy and scale than any previous deanonymization method — working from free text alone, without requiring structured data. Researchers tested LLM-based deanonymization across multiple datasets: Hacker News/LinkedIn cross-platform matching, Reddit user history splitting, and an Anthropic user questionnaire. In the Reddit experiment, recall (the proportion of users successfully identified) reached as high as 68%, with precision (accuracy of correct guesses) up to 90%. Unlike classical deanonymization techniques that required structured, schema-compatible datasets, LLM agents can reason across unstructured text, browse the web autonomously, and make probabilistic identity matches — a fundamentally new capability. The researchers warn this invalidates the longstanding assumption that pseudonymity provides adequate privacy protection for the average user.

**Key Data Points:**
- Recall (successful deanonymization rate) reached up to 68%; precision (accuracy when a match is made) up to 90% in best-case experiments
- In a Reddit movie subreddit experiment: users who discussed 10+ movies could be identified with 90% precision at a 48.1% recall rate — nearly half of prolific users unmasked
- In an Anthropic user questionnaire experiment: 7% of 125 anonymous participants were successfully identified from free-text answers alone — demonstrating the technique works even on very sparse data
- LLM agents outperformed classical "Netflix prize attack" baseline across all recall and precision metrics by a significant margin
- The researchers tested cross-platform matching (Hacker News posts + LinkedIn profiles) by stripping identifying references and running LLMs on the remaining text
- One co-author (Simon Lermen): "What we found is that these AI agents can do something that was previously very difficult: starting from free text, they can work their way to the full identity of a person."
- Researchers warn: governments could use these techniques to unmask online critics; corporations could build hyper-targeted ad profiles; attackers could assemble social engineering profiles at scale
- Proposed mitigations: platform rate limits on API access, detection of automated scraping, LLM provider guardrails against deanonymization requests
- Paper cites: "LLMs invalidate the assumption that pseudonymity provides adequate protection because targeted deanonymization would require extensive effort"

**Why It Matters:**
This research marks a step-change in the privacy threat landscape — one that emerges directly from the same AI agent capabilities being celebrated in enterprise contexts. The same LLM reasoning and web-browsing abilities that power agentic AI workflows can now be turned toward systematic privacy erosion at scale. For enterprise security teams, this is not a theoretical risk: any organization that has collected or published data about users — even anonymized or pseudonymized data — faces new re-identification exposure. For compliance and legal teams, this research will accelerate conversations about data retention policies, anonymization standards, and AI misuse liability. For professionals who use pseudonymous accounts for any purpose — whistleblowing, market research, competitive intelligence, sensitive community participation — the implicit privacy guarantee is now broken.

**Related Themes:** AI security, data privacy, deanonymization, LLM capabilities, enterprise security, cybersecurity, AI misuse, data compliance, privacy regulation
