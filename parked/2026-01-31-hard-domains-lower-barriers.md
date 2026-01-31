# Historically Hard Software Domains with Lower Barriers via AI

**Date:** 2026-01-31
**Status:** parked
**Tags:** ai-agents, systems-programming, compilers, databases, barrier-to-entry

## Summary

AI coding tools are lowering the barrier to entry for traditionally challenging areas of software development — compilers, systems programming, database internals, formal verification, GPU kernel optimization. The idea is that domains previously requiring years of specialized knowledge might now be more accessible to explore with AI assistance.

## Context

With AI coding agents becoming more capable (65% of developers using AI tools weekly per Stack Overflow 2025), there's a general sense that hard things are getting easier. The question: are there historically high-barrier domains that are now genuinely accessible enough to be worth exploring as a side interest?

## Key Observations

- **The classic hard domains:** Programming language design, compiler engineering, database internals, operating systems, distributed systems, formal verification, GPU kernel optimization, cryptographic implementations. These traditionally require deep specialized knowledge and years of ramp-up time.
- **AI is lowering barriers unevenly.** The application layer is getting dramatically easier. The systems layer — where correctness guarantees, performance, and deep domain knowledge matter — remains hard even for AI. Compilers, concurrency models, weak memory models, and GPU kernel optimization still have search spaces and verification challenges that LLMs struggle with.
- **Formal verification is a notable exception.** MIT's "vericoding" approach uses LLMs' improving mathematical capabilities to produce code with mathematical proof of correctness. This was historically limited to flight-control systems and crypto libraries due to cost. If this matures, it could open up a domain that was previously only accessible to specialists.
- **Conformance suites as an enabler.** If you're working with a new protocol or language, providing a language-agnostic conformance test suite lets AI agents implement against the spec effectively — even for technologies not yet in training data.
- **Debugging across complex codebases is where AI shines most.** Reasoning models can step through many layers of a codebase to find root causes. This applies to systems-level code too.
- **The skeptical view is worth noting.** AI tools "will get you across the pool; you might even get half a mile from shore, but there you are, in the middle of the lake, sitting on cardboard and duct tape, wishing you knew how to swim." The barrier is lower but the depth of these domains hasn't changed.
- **LLMs lag on new paradigms.** Code in new or niche paradigms is low-resource in training data. LLMs have been found to fail to utilize new security features in compiler and toolkit updates, still relying on legacy methods.

## Decision

Parked. The premise is sound — AI does lower barriers to exploring hard domains — but so far nothing here has sparked genuine personal interest. A lower barrier doesn't create motivation. Not interested in building a database or writing a compiler just because it's now more feasible.

## References

- [AI Coding Is Now Everywhere (MIT Technology Review)](https://www.technologyreview.com/2025/12/15/1128352/rise-of-ai-coding-developers-2026/)
- [My LLM Coding Workflow Going Into 2026 (Addy Osmani)](https://addyosmani.com/blog/ai-coding-workflow/)
- [2025: The Year in LLMs (Simon Willison)](https://simonwillison.net/2025/Dec/31/the-year-in-llms/)
- [Challenges and Paths Towards AI for Software Engineering (arxiv)](https://arxiv.org/html/2503.22625v1)
- [Coding With AI: From a Reflection on Industrial Practices (arxiv)](https://www.arxiv.org/pdf/2512.23982)
- [Ask HN: Are AI Dev Tools Lowering the Barrier to Entry?](https://news.ycombinator.com/item?id=42934456)
- [Coding With LLMs in 2026: The Model Matters More Than the Prompts](https://boredhacking.com/coding-with-llms-2026/)
- [Natural Language Programming Is Lowering Software Development's Barrier to Entry](https://segunakinyemi.com/blog/natural-language-programming/)
