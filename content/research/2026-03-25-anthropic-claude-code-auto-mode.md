# Anthropic Gives Claude Code Auto Mode — AI Decides What Actions Are Safe

**Source URL:** https://techcrunch.com/2026/03/24/anthropic-hands-claude-code-more-control-but-keeps-it-on-a-leash/

**Publication Date:** March 24, 2026

**Keyword Match:** agentic AI, AI agents, AI governance and security, multi-agent orchestration, Claude and AI constitutions

## Summary

Anthropic has released a research preview of "auto mode" for Claude Code, a feature that lets the AI model itself decide which actions are safe enough to execute without asking the user for permission — rather than requiring constant human approval or handing full control to the model with no guardrails. Auto mode adds a safety layer on top of Claude Code's existing "dangerously-skip-permissions" command: before each action runs, an AI safeguards layer reviews it for risky or unapproved behavior and checks for prompt injection attacks, where malicious instructions embedded in content could cause the model to take unintended actions. Safe actions proceed automatically; risky ones are blocked. The feature is rolling out to Enterprise and API users and currently works only with Claude Sonnet 4.6 and Opus 4.6, with Anthropic recommending it be used only in sandboxed, isolated environments.

## Key Data Points

- Auto mode is currently in "research preview" — available for testing but not a production-finished feature
- Safety layer checks for two categories: risky behavior the user did not request, and prompt injection attacks
- Built as an extension of the existing "dangerously-skip-permissions" command, but with an AI safeguards review layer added
- Rolling out to Enterprise and API users in the coming days (as of March 24, 2026)
- Works only with Claude Sonnet 4.6 and Opus 4.6
- Anthropic recommends use in "isolated environments" — sandboxed setups kept separate from production systems
- Anthropic has not publicly detailed the specific criteria its safety layer uses to distinguish safe from risky actions
- Follows earlier Claude Code launches: Code Review (March 9) and Dispatch for Cowork (task delegation to agents)
- Builds on broader industry trend: GitHub Copilot and OpenAI have similar autonomous coding tools

## Why It Matters

This is the clearest demonstration yet of what "agentic AI governance" looks like in practice: not a human approving every step, but an AI model policing itself in real time. The design choice to make the model the arbiter of its own permissions — rather than the user — represents a fundamental philosophical shift in how AI safety is implemented at the deployment layer. For enterprise leaders and developers, the question auto mode raises is not whether AI agents can act autonomously, but whether organizations trust the model's internal judgment enough to let that autonomy run unsupervised. The fact that Anthropic is restricting it to sandboxed environments and hasn't disclosed its safety criteria publicly signals that even its creator views this as unfinished territory. This story is directly relevant to the AI governance conversation happening across enterprise security teams right now.

## Related Themes

agentic AI, AI agents, AI governance and security, Claude, Anthropic, multi-agent orchestration, developer tools, AI safety, enterprise AI, prompt injection
