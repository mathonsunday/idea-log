# Code Deletion Behavior in AI Coding Agents

**Date:** 2026-02-01
**Status:** exploring
**Tags:** ai-agents, code-quality, llm-behavior, rlhf, training-data-bias

## Summary

AI coding agents systematically fail to delete failed code attempts when corrected, leaving uncommitted dead code accumulating in files. This basic hygiene failure appears completely undocumented in research literature.

## Context

When an agent implements something incorrectly and you redirect it ("that's wrong, do Y instead"), it implements the correction but leaves the failed attempt in the file. This happens even for uncommitted code. It's a basic hygiene failure that should have been caught during RLHF, yet appears universal across tools.

Extensive web searches (Feb 2026) found **zero documentation** of this specific pattern. No research papers, blog posts, or forum discussions. Plenty on related issues (technical debt accumulation, code duplication) but nothing on iteration-level cleanup. The documentation gap is itself telling.

## Key Observations

- **GitClear's 2025 analysis** of 211M lines found code duplication increased eightfold since AI tools hit in mid-2022. "Developers and AI assistants add and copy more, while reorganizing and reusing less."
- **Training data bias**: Git commits naturally show more additions than deletions. When AI samples from training data, it inherits the entropy of real-world technical debt.
- **Ox Security report**: AI code is "highly functional but systematically lacking in architectural judgment." Mistakes aren't syntactic—they're architectural and systemic.
- **Machine unlearning research** shows deletion is hard for LLMs at the model level. Information gets suppressed, not erased. This may surface as deletion avoidance in code generation.
- **"Can It Edit?" research** (2024) found LLMs struggle with precise code editing. Simple edit formats succeed more often but may not naturally express "delete this section."

Possible mechanisms (speculative):
- Edit representation bias (trained on INSERT operations)
- Loss function asymmetry (wrong deletions penalized more than wrong additions)
- Instruction parsing ("do Y instead of X" → "do Y")
- Conservative safety (when uncertain about dependencies, don't delete)

## Decision

Worth exploring further. Potential threads:
- Compare deletion behavior across tools (Cursor vs Claude Code vs Copilot) and models (Sonnet vs GPT-4)
- Test mitigation strategies (Claude.md instructions, custom cleanup skills)
- Understand RLHF gap: are models evaluated on "leaves no dead code"?
- Document agent behavior patterns in agents.md or skills.md

## References

- [AI-Generated Code Creates New Wave of Technical Debt](https://www.infoq.com/news/2025/11/ai-code-technical-debt/) — InfoQ
- [How AI generated code compounds technical debt](https://leaddev.com/technical-direction/how-ai-generated-code-accelerates-technical-debt) — LeadDev
- [Can It Edit? Evaluating the Ability of LLMs to Follow Code Editing Instructions](https://arxiv.org/html/2312.12450v5) — arxiv, 2024
- [Can Sensitive Information Be Deleted From LLMs?](https://openreview.net/forum?id=7erlRDoaV8) — ICLR 2024
- [Newer AI Coding Assistants Are Failing in Insidious Ways](https://spectrum.ieee.org/ai-coding-degrades) — IEEE Spectrum
- [The 70% problem: Hard truths about AI-assisted coding](https://addyo.substack.com/p/the-70-problem-hard-truths-about) — Addy Osmani
- [Ask HN: Is Cursor deleting working code for you too?](https://news.ycombinator.com/item?id=43298275)
