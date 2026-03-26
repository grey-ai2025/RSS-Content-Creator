---
source_file: content/research/2026-03-25-mozilla-cq-stack-overflow-agents.md
keywords_file: content/seo/2026-03-25-keywords.md
status: ranked
created_date: 2026-03-25
---

## HEADLINE
A Mozilla developer has released an open-source tool that lets AI agents share discovered knowledge across instances — solving the problem where every agent independently re-solves the same problems because there is no mechanism for knowledge to persist after training cutoff.

## KEY FACTS
- Every AI agent in a multi-agent system currently starts from the same training cutoff — when one agent discovers a novel solution, no other agent ever benefits from it
- The tool (cq) lets agents query a shared knowledge commons before tackling unfamiliar tasks, then contribute new findings back
- Available as a plugin for Claude Code and OpenCode; includes MCP server for local knowledge storage and an API for team-level sharing
- Described as a "proof of concept" — not production-ready; developer community raised prompt injection and data poisoning risks
- Source credibility: Mozilla developer, open-source (verifiable on GitHub), Hacker News developer reception

## GREY AI ANGLE
Every redundant token an agent spends re-solving a known problem is a cost, a latency, and a reliability risk. For teams building multi-agent workflows, the knowledge-sharing gap is not theoretical — it is the reason agents fail at the same edge cases repeatedly. This tool asks the governance question behind it: when agents share a knowledge commons, who audits what goes in?

## HOOK OPTIONS

**Provocative:** Your AI agents are solving the same problems every single day — and sharing nothing with each other. You're paying for that ignorance in compute and errors.

**Binary:** Single agent in isolation: re-discovers every edge case from scratch, learns nothing across projects. Agents with shared knowledge layer: queries what others already found, contributes new discoveries back, compounds knowledge over time. Two architectures — and the gap between them is already costing enterprise teams real money.

**Contrarian:** The most expensive inefficiency in multi-agent AI deployments isn't compute or latency. It's agents that can't tell each other what they've already learned — and most enterprise AI stacks have no mechanism to fix that.

## SUGGESTED FORMAT
carousel
Reasoning: Three distinct points — the problem (agents re-solving known issues at scale), the mechanism (shared knowledge commons architecture), and the governance implication (who audits shared knowledge for poisoning/injection?) — each support a slide; the concrete cost framing ("you're paying for this") maps to the benchmark's highest-engagement personal-threat hook pattern.

## KEYWORDS
- Trending topics to weave in: multi-agent orchestration, Model Context Protocol (MCP), agentic AI
- Hashtags: #AIAgents #AgenticAI #ArtificialIntelligence #MachineLearning #PromptEngineering

## RAW MATERIAL
Concrete example from the tool's documentation: if one agent discovers "Stripe returns 200 with an error body for rate-limited requests," every subsequent agent benefits from that discovery rather than hitting the same undisclosed edge case. The current workaround — manually updating claude.md or agents.md files — does not cross-pollinate knowledge between different projects or teams. The MCP server is central to the architecture: cq is being built from the ground up as MCP-compatible, positioning it to work within the Model Context Protocol infrastructure that is rapidly becoming the enterprise standard. Developer concern framing from Hacker News: models do not reliably track their own reasoning steps, which creates risk of junk or incorrect knowledge accumulating in the shared commons at scale.
