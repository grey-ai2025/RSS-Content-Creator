---
date: 2026-02-25
title: "Anthropic Accuses Chinese AI Labs of Running Industrial-Scale Distillation Attacks on Claude"
source_url: "https://techcrunch.com/2026/02/23/anthropic-accuses-chinese-ai-labs-of-mining-claude-as-us-debates-ai-chip-exports/"
source_name: "TechCrunch"
keywords: [Anthropic, Claude, AI safety, AI governance, AI regulation, LLM, open source AI, AI chip stocks]
---

# Summary

A major U.S. AI company has publicly accused three Chinese AI laboratories of orchestrating coordinated, industrial-scale "distillation attacks" against its flagship AI model — using over 24,000 fraudulent accounts to generate more than 16 million exchanges designed to extract the model's most advanced capabilities and transfer them to competing Chinese models. Distillation is an established AI training technique that allows developers to train smaller, cheaper models by learning from the outputs of a more powerful model; when used against a competitor's model without authorization, it functions as a form of capability theft.

The company identified three labs behind the attacks: one with roots in the Chinese deep learning research community whose models generated 150,000 exchanges focused on foundational logic and censorship-safe alternatives; one with over 3.4 million exchanges targeting agentic reasoning, tool use, coding, and computer vision; and one that generated 13 million exchanges focused on agentic coding and tool orchestration, with nearly half its traffic redirected to siphon capabilities from the company's newest model at the moment of its launch. The company says it has developed new detection methods that allowed it to identify these attacks in real time and is calling on the broader AI industry, cloud providers, and policymakers to coordinate a response.

The accusations arrive at a politically charged moment, as the U.S. debates how strictly to enforce export controls on advanced AI chips to China. The company explicitly argued that distillation attacks reinforce the case for chip export restrictions, noting that the scale of extraction it observed "requires access to advanced chips." Former CrowdStrike co-founder and cybersecurity expert Dmitri Alperovitch confirmed the pattern: "It's been clear for a while now that part of the reason for the rapid progress of Chinese AI models has been theft via distillation of U.S. frontier models. Now we know this for a fact."

# Key Data Points

- More than 24,000 fraudulent accounts were created across the three Chinese AI labs to access the targeted AI model
- Total exchanges generated: over 16 million
- Lab A generated 150,000+ exchanges targeting foundational logic and censorship-safe query alternatives
- Lab B generated 3.4 million+ exchanges targeting agentic reasoning, tool use, coding, data analysis, and computer vision
- Lab C generated 13 million+ exchanges targeting agentic coding, tool use, and orchestration — and redirected nearly half its traffic to target the newest model version at launch
- The targeted capabilities were specifically the model's "most differentiated" functions: agentic reasoning, tool use, and coding
- OpenAI separately accused one of the same Chinese labs of using distillation to mimic its products, in a memo to House lawmakers earlier in February 2026
- The company called on "a coordinated response across the AI industry, cloud providers, and policymakers"
- Argument made: models built through illicit distillation may not retain safety guardrails, creating proliferation risk for dangerous capabilities (e.g., bioweapons, cyberattacks)
- The Trump administration in December 2025 formally allowed export of advanced AI chips (H200) to China; critics argue this loosening increases Chinese AI capacity

# Professional Relevance

For enterprise technology and security professionals, this story highlights that the competitive threat from AI model distillation is not a hypothetical — it is an active, ongoing form of intellectual property exfiltration happening at scale right now. Organizations building AI products on top of frontier models should understand that their competitive moat may be more vulnerable than they realize, and that AI governance frameworks will increasingly need to address not just how AI is used internally but how it is protected from external extraction.

# Potential Angles

- The AI arms race has its first major IP theft scandal: when 16 million fake conversations are used to steal the world's most capable AI model's skills, the competitive dynamics of the global AI industry change permanently
- Why AI safety guardrails are also a proliferation risk: models built through illicit distillation don't inherit the safety constraints of the original — meaning dangerous capabilities can spread without any of the protections that were designed to contain them
- The chip export debate just got a new argument: if distillation attacks require advanced chips, then controlling chip access is also a way to limit the scale of AI model theft — a point now backed by documented evidence
- Agentic AI is the prime target: the fact that all three attacks specifically focused on agentic reasoning, tool use, and coding tells us something important about where the real competitive value in frontier AI systems currently lives
