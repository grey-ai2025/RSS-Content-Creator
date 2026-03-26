# Mozilla Developer Builds "Stack Overflow for Agents" — A Shared Knowledge Layer for Multi-Agent Systems

**Source URL:** https://arstechnica.com/ai/2026/03/mozilla-dev-introduces-cq-a-stack-overflow-for-agents/

**Publication Date:** March 24, 2026

**Keyword Match:** multi-agent orchestration, Model Context Protocol (MCP), AI agents, agentic AI

## Summary

Mozilla developer Peter Wilson has released an early-stage open-source tool called "cq" — described as a "Stack Overflow for agents" — designed to solve a fundamental inefficiency in multi-agent AI systems: every agent is independently solving the same problems from scratch because there is no mechanism for sharing discovered knowledge across agent instances after the model's training cutoff. Cq works by letting agents query a shared commons of verified runtime knowledge before tackling unfamiliar tasks (such as API integrations or CI/CD configurations), and contributing new discoveries back to that commons when they encounter novel solutions. The system is currently available as a plugin for Claude Code and OpenCode, includes an MCP server for local knowledge libraries, an API for team-level knowledge sharing, and a human review UI. Wilson announced the project on Mozilla.ai's blog and Hacker News, where developers acknowledged the value proposition but raised serious concerns about security (prompt injection risks, data poisoning) and accuracy (models do not reliably track their own reasoning steps).

## Key Data Points

- cq is available now as a plugin for Claude Code and OpenCode
- Core infrastructure: an MCP server for local knowledge storage, an API for cross-team sharing, and a UI for human review
- Primary problem addressed: coding agents repeatedly solve the same issues because training cutoffs prevent knowledge sharing between agent instances
- Example use case: if one agent discovers "Stripe returns 200 with an error body for rate-limited requests," every subsequent agent benefits from that discovery rather than re-solving it
- Wilson describes cq as currently superior to the current workaround: manually updating claude.md or agents.md files based on trial and error — a solution that does not cross-pollinate knowledge between projects
- Current state: described as a "proof of concept" — not production-ready
- Open-source: available on GitHub at mozilla-ai/cq
- Hacker News response: mixed — broad agreement on the problem, but significant concerns raised about:
  - Prompt injection vulnerabilities
  - Data poisoning risks
  - Model unreliability in tracking steps it takes (potential for junk knowledge at scale)
- Not alone in this space: multiple projects are attempting to address the same cross-agent knowledge problem at different levels of the stack

## Why It Matters

Cq represents one of the clearest articulations of a problem that will define multi-agent orchestration in 2026: as enterprises deploy fleets of AI agents, the inefficiency of each agent re-solving known problems is not just a performance issue — it is a cost issue and a reliability issue. Every redundant token spent is compute that could be directed elsewhere, and every agent that hits the same undiscovered edge case represents a governance risk. The MCP server integration is significant: it means cq is being built from the ground up to be compatible with the Model Context Protocol infrastructure that is rapidly becoming the standard for cross-agent communication. For practitioners building multi-agent workflows, this story is a leading indicator of where the tooling ecosystem is heading — and for enterprise architects, it raises the question of whether shared agent knowledge layers will eventually need the same security controls as shared data systems.

## Related Themes

multi-agent orchestration, Model Context Protocol (MCP), AI agents, agentic AI, developer tools, open source, AI governance and security, Claude Code, enterprise AI, knowledge management
