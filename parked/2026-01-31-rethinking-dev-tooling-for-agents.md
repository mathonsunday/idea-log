# Rethinking Developer Tooling for AI Agents

**Date:** 2026-01-31
**Status:** parked
**Tags:** ai-agents, developer-tools, IDEs, CLI, developer-experience

## Summary

Do command line tools, IDEs, and code organization paradigms need to be fundamentally rethought for coding agents? Based on what's actually happening, the answer is mostly no. Agents work fine with existing developer interfaces — filesystems, bash, grep, git. The real innovation in developer tooling right now is about making existing tools faster (Rust rewrites), not about redesigning them for LLMs.

## Context

After exploring whether agents need new tool paradigms, the evidence points toward agents being surprisingly capable with the tools humans already use. The most striking example is Vercel discovering that stripping their agent down from many specialized tools to just a filesystem and bash tool improved performance from 80% to 100% success rate while cutting costs by 75%. LLMs have been trained on massive amounts of code that uses standard Unix tools — grep, cat, find, awk are native operations for them, not bolted-on behaviors.

## Key Observations

### Agents don't need new interfaces — they already know existing ones

Vercel spent months building a sophisticated agent with specialized tools, heavy prompt engineering, and careful context management. Then they deleted most of it and gave the agent a bash shell and a filesystem. It got simpler and better at the same time. Their conclusion: "Every agent needs filesystem and bash. If you're building an agent, resist the urge to create custom tools. Instead, ask: can I represent this as files?" Their sales call summarization agent went from ~$1.00 to ~$0.25 per call on Claude Opus 4.5 with better output quality.

### The actual innovation in dev tooling is speed, not AI-friendliness

The big developer tooling story of 2025-2026 is Rust rewrites making existing tools faster, not redesigning tools for agents:

- **Biome.js** replaced ESLint/Prettier with 340+ linting rules and type-aware linting that doesn't invoke the TypeScript compiler.
- **Rolldown** (Rust-native bundler) is replacing Rollup in Vite.
- **Turbopack** rethought bundling around incremental computation and persistent caching.
- **Rspack** delivered Rust-level performance while staying compatible with existing Webpack configs.
- **fd, ripgrep, bat, zoxide** — Rust rewrites of standard Unix tools (find, grep, cat, cd) that are faster and more ergonomic.
- **OpenAI rewrote Codex CLI in Rust** for security and performance, moving from React/TypeScript/Node.

The driver is scale (monorepos, micro-frontends, CI reliability) and developer experience as a business metric — not AI agent compatibility. Most developers didn't consciously choose Rust tooling; their frameworks made the choice (Next.js integrated SWC/Turbopack, Vite moved to Rolldown).

### "Agentic IDEs" are additions, not replacements

The "agentic IDE" trend (Cursor, Kiro, Windsurf) is about adding agent capabilities on top of existing interfaces, not replacing them. Cursor is built on VS Code. Kiro slots into existing VS Code setups. Claude Code lives in the terminal. The pattern is: keep the existing interface, add agent orchestration alongside it. Developers want memory, human-in-the-loop controls, and reliability — not a fundamentally different coding interface.

### Terminal is re-emerging, but it's the same terminal

Claude Code and Gemini CLI brought AI into the command line, but the command line itself didn't change. Agents use the same bash, the same filesystem, the same git. The "agentic CLI era" is really just agents that happen to work in the terminal — not a rethinking of what the terminal is.

## Decision

Parked. There doesn't appear to be a significant need or push to rethink developer tooling interfaces for agents. Agents work well with existing tools because LLMs were trained on billions of examples of those tools being used. The actual tooling innovation is about performance (Rust rewrites) and adding agent orchestration alongside existing interfaces — not about making interfaces more LLM-friendly.

## References

- [We Removed 80% of Our Agent's Tools (Vercel)](https://vercel.com/blog/we-removed-80-percent-of-our-agents-tools)
- [How to Build Agents with Filesystems and Bash (Vercel)](https://vercel.com/blog/how-to-build-agents-with-filesystems-and-bash)
- [vercel-labs/bash-tool (GitHub)](https://github.com/vercel-labs/bash-tool)
- [Deep Dive: Why Rust-Based Tooling is Dominating JavaScript in 2026](https://dev.to/dataformathub/deep-dive-why-rust-based-tooling-is-dominating-javascript-in-2026-3dbl)
- [Rust JS Tooling 2025: Why Biome, Oxc, and Rolldown Change Everything](https://dev.to/dataformathub/rust-js-tooling-2025-why-biome-oxc-and-rolldown-change-everything-20i3)
- [OpenAI's Codex CLI Goes Native, Drops Node for Rust (InfoQ)](https://www.infoq.com/news/2025/06/codex-cli-rust-native-rewrite/)
- [10 Things Developers Want from Agentic IDEs in 2025 (RedMonk)](https://redmonk.com/kholterhoff/2025/12/22/10-things-developers-want-from-their-agentic-ides-in-2025/)
- [The Best Agentic IDEs Heading Into 2026 (Builder.io)](https://www.builder.io/blog/agentic-ide)
- [AI Coding Tools in 2025: Welcome to the Agentic CLI Era (The New Stack)](https://thenewstack.io/ai-coding-tools-in-2025-welcome-to-the-agentic-cli-era/)
- [AI IDEs or Autonomous Agents? Measuring Impact (arxiv)](https://arxiv.org/html/2601.13597)
