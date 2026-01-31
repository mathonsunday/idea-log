# Memory Bank Replacement for Coding Agents

**Date:** 2026-01-31
**Status:** explored
**Tags:** ai-agents, developer-tools, context-management, llms, art

## Summary

The "memory bank" pattern — structured markdown files that give coding agents persistent project context across sessions — is widely used but has known scaling problems. The industry is moving toward more sophisticated alternatives: hierarchical memory systems, skills-based approaches, and context compression. This is an interesting and active area of research, just not one I'm personally excited to work in right now.

## Context

The memory bank pattern was popularized by Cline, where a set of structured markdown files (project brief, active context, system patterns, tech context, progress) are read by the agent at the start of every session to reconstruct project understanding. The pattern has been adopted across tools (Cursor, Claude Code, etc.) because it's simple and works. The problem: it eats context fast. Every session starts by loading all memory bank files, consuming a significant chunk of the context window before any real work begins.

A coworker is actively working in this space — converting memory bank content to skills (invocable capabilities rather than passive context), writing leaner CLAUDE.md files, and working on a project context repo. The related Jarvis Decomp project is at https://github.com/ConsultingMD/prj-monoliths-reckoning.

## Key Observations

- **The naive approach doesn't scale.** Loading all project context into every session is a brute-force strategy. Nearly 65% of enterprise AI failures in 2025 were attributed to context drift or memory loss during multi-step reasoning, suggesting the problem is real but the current solutions aren't working.
- **The industry is fragmenting into multiple approaches.** MemGPT/Letta treats context like OS virtual memory (RAM + disk). LangGraph + MongoDB provides database-backed persistent stores. Graph-structured memory (Graphiti/Zep, MAGMA) enables relational queries. RL-trained memory management (MemRL, MemSearcher) lets agents learn *what* to remember. Git-style versioning (Git-Context-Controller) applies branch/merge/commit to context.
- **Selective memory matters more than total recall.** Research shows indiscriminate storage propagates errors and degrades long-term performance. Utility-based and retrieval-history-based deletion yield up to 10% performance gains over naive strategies.
- **Skills as an alternative to passive context.** Converting domain knowledge into invocable skills rather than context dumps is a promising direction — the agent calls what it needs rather than loading everything upfront.
- **Recent research is accelerating.** "Context as a Tool" (Nov 2025) specifically targets SWE agents. MAGMA, EverMemOS, and MemRL (Jan 2026) all propose new architectures. A comprehensive survey ("Memory in the Age of AI Agents") notes the landscape is highly fragmented with loosely defined terminology.
- **Expanding context windows isn't the answer.** Llama 4 has a 10M token window, but the consensus is hierarchical memory management is more cost-effective and reliable than simply expanding windows.

## Decision

Exploring — but solely as an art project, not as tooling. The technical landscape is interesting source material for interactive fiction: what does it feel like to be a being whose memory is a sliding window? What happens when retrieval is imperfect and you confidently state the wrong thing? These are more compelling to me as dramatic questions than as engineering problems.

A coworker is already actively pursuing the skills-based tooling angle. The dual-audience documentation exploration is upstream of the tooling problem. My interest here is in dramatizing these memory dynamics, not benchmarking them.

**Active project:** [memory-theater](https://github.com/mathonsunday/memory-theater) — an interactive art installation where you converse with a character (Sable) whose memory behaves differently in each "act." Each act implements a different memory architecture from current AI research (sliding context window, episodic memory with retrieval noise, etc.).

## References

- [Cline Memory Bank (official docs)](https://docs.cline.bot/prompting/cline-memory-bank)
- [Memory Bank: How to Make Cline an AI Agent That Never Forgets](https://cline.bot/blog/memory-bank-how-to-make-cline-an-ai-agent-that-never-forgets)
- [Design Patterns for Long-Term Memory in LLM-Powered Architectures (Serokell)](https://serokell.io/blog/design-patterns-for-long-term-memory-in-llm-powered-architectures)
- [A Survey on the Memory Mechanism of LLM-based Agents (ACM)](https://dl.acm.org/doi/10.1145/3748302)
- [Persistent Memory in LLM Agents (Emergent Mind)](https://www.emergentmind.com/topics/persistent-memory-for-llm-agents)
- [AI-Native Memory and the Rise of Context-Aware AI Agents](https://ajithp.com/2025/06/30/ai-native-memory-persistent-agents-second-me/)
- [LLM Development Services in 2026: Long-Context Memory (Calibraint)](https://www.calibraint.com/blog/llm-development-services-in-2026)
- [Awesome Memory for Agents paper list (TsinghuaC3I)](https://github.com/TsinghuaC3I/Awesome-Memory-for-Agents)
- Jarvis Decomp project: https://github.com/ConsultingMD/prj-monoliths-reckoning
