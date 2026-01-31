# Agentic Persistence & Orchestration Tools

**Date:** 2026-01-31
**Status:** idea
**Tags:** ai-agents, developer-tools, persistence, orchestration

## Summary

A coworker shared a write-up on composable tools for always-on AI engineering partners — solving context loss, session continuity, multi-agent coordination, and memory across layers.

## Context

The core friction points in agentic engineering today: context windows fill up, sessions end and lose continuity, single-threaded execution, and manual orchestration. The write-up covers six tools attacking different parts of this: Beads (git-native issue tracking), Superpowers (auto-triggering skills), Episodic Memory (semantic search over conversations), Private Journal MCP (structured thinking space), Claude Code Hooks (multi-agent observability), and MCPProxy (federated MCP aggregation).

## Key Observations

- The "persistence layer stack" framing is useful: task (Beads), conversation (Episodic Memory), fact (Memory Server), reasoning (Private Journal) — each with different retrieval patterns
- "Tree of Claudes" pattern: orchestrator delegates to child agents, receives summaries, main loop stays clean
- Auto-triggering skills (Superpowers) inverts discovery — check all possibly-relevant skills rather than requiring the user to know what exists
- Core philosophy: augmentation not replacement — agents handle mechanical/context-heavy work, humans retain judgment and intent

## Decision

Worth exploring further. Interesting areas to dig into:
- Git-native issue tracking for personal projects (Beads concept)
- Episodic memory for preserving decision reasoning across sessions
- Multi-agent orchestration patterns

## References

- Coworker's write-up shared via internal doc
- Beads, Private Journal MCP, Superpowers plugin referenced in original
