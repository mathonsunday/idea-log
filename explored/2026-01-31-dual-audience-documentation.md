# Dual-Audience Documentation: Writing for Humans and LLMs

**Date:** 2026-01-31
**Status:** exploring
**Tags:** documentation, llms, developer-experience, ai-agents

## Summary

Documentation that works well for humans doesn't automatically work well for LLMs, and the gap is widening as AI agents become primary consumers of docs. This is an emerging area focused on making documentation better for both audiences simultaneously.

## Context

While looking at how ConsultingMD/omnibus tracks documentation health and maturity (quality scores, canonicity levels, Diataxis form types), the question came up: is documentation that's effective for human reading the same as documentation that's effective for LLMs? Research and industry practice say no — and the divergence is growing.

This problem space is more personally interesting to me than the "memory bank replacement" thread. That thread is about efficiently sharing domain knowledge with LLMs so they do the right thing. This thread is about making the documentation itself better for both humans AND coding agents — it's upstream of the memory bank problem.

## Key Observations

- **Humans and LLMs want different things.** Humans benefit from narrative, visual hierarchy, and creative headings. LLMs need strict heading hierarchy, consistent terminology (no synonym switching), answer-first structure, and short self-contained paragraphs that can be extracted as units.
- **`llms.txt` is emerging as an industry convention.** Inspired by `robots.txt`, it's a plain Markdown file at a site root that indexes documentation for LLM consumption. An extended `llms-full.txt` variant concatenates entire doc sites into one file. Mintlify, GitBook, and Redocly auto-generate these.
- **Gartner predicts 30%+ of API demand will come from AI agents by 2026**, not human developers. 84% of developers use or plan to use AI tools (Stack Overflow 2025), but 46% don't trust AI accuracy — partly a doc quality problem.
- **PNAS Nexus research (Oct 2025, n=10,462) found a tension**: the concise, extractable, answer-first style that helps LLMs may actually produce shallower human understanding. Optimizing for LLM consumption could degrade the learning experience.
- **Structured metadata is the bridge.** Frontmatter annotations (like what omnibus does with quality, canonicity, form, tags) make docs more LLM-parseable without hurting human readability. The Diataxis `form` field is useful here — an LLM consuming a doc tagged REFERENCE knows to treat it differently than one tagged TUTORIAL.
- **Markdown is the common ground** — parseable by both humans and machines, unlike rich HTML layouts.

## Decision

Exploring, not currently building. This sits at the intersection of documentation quality and the shift toward AI-agent-driven developer workflows — worth continuing to learn about.

## References

- [The Future of Documentation: From Human-Readable to LLM-Friendly (Zylo Systems)](https://blog.zylosystems.com/posts/documentation-for-llms)
- [LLM-Friendly Documentation: Creating Content AI Can Understand (Aron Hack)](https://aronhack.com/llm-friendly-documentation-creating-content-that-ai-can-understand-and-process-effectively/)
- [How to Optimize Your Docs for LLMs (Redocly)](https://redocly.com/blog/optimizations-to-make-to-your-docs-for-llms)
- [What is llms.txt? (GitBook)](https://www.gitbook.com/blog/what-is-llms-txt)
- [llms.txt (Mintlify)](https://www.mintlify.com/docs/ai/llmstxt)
- [PNAS Nexus: LLMs vs Web Search on Depth of Learning](https://academic.oup.com/pnasnexus/article/4/10/pgaf316/8303888)
- [The Definitive Guide to LLM-Optimized Content (Averi AI)](https://www.averi.ai/breakdowns/the-definitive-guide-to-llm-optimized-content)
- [LLM Content Optimization Best Practices 2026 (Fibr AI)](https://fibr.ai/geo/llm-content-optimization-best-practices-2026)
