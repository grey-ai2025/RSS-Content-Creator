---
date: 2026-03-05
source: Ars Technica
url: https://arstechnica.com/security/2026/03/llms-can-unmask-pseudonymous-users-at-scale-with-surprising-accuracy/
keywords: AI security and adversarial threats, AI agents
---

# LLMs Can Now Deanonymize Pseudonymous Users at Scale — With Up to 90% Precision

## Summary

A peer-reviewed research paper has demonstrated that large language models can strip pseudonymity from online users at a scale and accuracy that classical deanonymization methods cannot match — with precision rates as high as 90% and recall rates up to 68%. The research, conducted across multiple social media datasets, shows AI agents can correlate accounts across platforms (e.g., Hacker News and LinkedIn profiles, Reddit subreddits) and identify real-world identities from unstructured free text — something that previously required structured datasets with matching schemas. The implications for online privacy are significant: pseudonymity, which millions of people rely on for sensitive discussions, may now be functionally inadequate as a privacy measure.

The mechanism is the same capability that makes AI agents powerful in other contexts: they can browse the web, reason about identities across multiple information sources, and verify matches using the same logic a skilled human investigator would apply — at machine speed and scale. A co-author of the paper noted this is "a pretty new capability" — prior approaches required structured data, not free text. In one experiment, researchers identified 7% of 125 Anthropic survey participants from their interview transcripts alone. In another, users who shared more than 10 movies in Reddit communities could be identified with 90% precision in 48.1% of cases.

The researchers propose platform-level mitigations (API rate limits, detection of automated scraping, bulk data export restrictions) and suggest LLM providers could build guardrails to detect deanonymization requests. Neither intervention has been implemented at scale. The paper warns that governments could use these techniques to unmask online critics, corporations to assemble hyper-targeted advertising profiles, and attackers to build personalized social engineering targets.

## Key Data Points

- Recall rate (percentage of pseudonymous users successfully identified): up to 68%
- Precision rate (accuracy of identifications made): up to 90%
- In a Reddit movie-discussion experiment, users who shared 10+ films could be identified at 90% precision in 48.1% of cases
- Researchers identified 7% of 125 Anthropic survey participants from anonymized interview transcripts alone
- Classical deanonymization (e.g., the 2008 Netflix prize attack) required structured data with matching schemas; LLMs work from unstructured free text
- AI agents in this context autonomously browse the web, extract identity signals, and verify matches — no human required
- Co-author Simon Lermen: "Starting from free text (like an anonymized interview transcript) they can work their way to the full identity of a person"
- LLM-based deanonymization substantially outperforms classical methods across all tested precision thresholds
- Risk vectors identified: government surveillance of critics, hyper-targeted advertising, personalized social engineering at scale
- Proposed mitigations: API rate limits, automated scraping detection, LLM guardrails — none yet implemented at scale

## Relevance

This story sits directly at the intersection of AI security, agent capability, and enterprise risk. For LinkedIn's professional audience — particularly those in cybersecurity, legal, HR, and compliance roles — the implication is concrete: internal whistleblowers, anonymous employee survey respondents, and pseudonymous company reviewers on platforms like Glassdoor can now be identified using freely available LLM tools. This is an adversarial use of the same agent capabilities that enterprises are deploying for productivity. The story is technically credible (peer-reviewed research), practically alarming, and underreported relative to its significance.

## Related Themes

AI security, adversarial AI, privacy, deanonymization, AI agents, LLMs, online privacy, enterprise risk, cybersecurity
