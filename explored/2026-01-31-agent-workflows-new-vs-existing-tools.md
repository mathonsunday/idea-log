# AI Agents Making Historically Impractical Dev Tools Viable

**Date:** 2026-01-31
**Status:** exploring
**Tags:** ai-agents, developer-tools, mutation-testing, formal-verification, openrewrite, LST

## Summary

Some software development techniques have always been powerful in theory but impractical to use regularly — formal verification, mutation testing, lossless semantic trees. AI agents might be the catalyst that makes these approaches viable by handling the complexity and tedium that kept them out of everyday use. This is a different question from how agents integrate with existing tools — it's about whether agents can fundamentally change what tools and techniques are part of standard practice.

## Context

My mutation-test-gen projects ([mutation-test-gen](https://github.com/mathonsunday/mutation-test-gen) for TypeScript, [go-mutation-test-gen](https://github.com/mathonsunday/go-mutation-test-gen) for Go) were inspired by Meta's ACH system. Those projects are a concrete example: mutation testing was a research curiosity for decades, and agents are turning it into a production tool. I'm looking for more examples of this pattern — powerful-but-impractical techniques becoming accessible through agents.

## Key Observations

### Lossless Semantic Trees replacing ASTs for code transformation

Moderne/OpenRewrite uses LSTs that preserve exact formatting, byte ranges, and full type information for every code element. This lets agents perform "minimally invasive" refactors that honor existing style guides and do semantic searches (e.g., finding all instances of a method even when aliased or shadowed — impossible with text-based grep). Choice Hotels used LST-based recipes to automate large-scale framework migrations across thousands of repositories. Agents can invoke 3,500+ deterministic, composable OpenRewrite recipes — giving them a fundamentally richer view of code than AST or text-based approaches.

### Mutation-guided testing replacing coverage-driven testing

Meta's ACH moved from coverage-driven testing (did this line execute?) to mutation-guided testing (would this test catch this bug?). A specialized Equivalence Detector agent (Llama 3.1 70B + static analysis) filters semantically redundant mutants with 0.95 precision and 0.96 recall — solving the equivalent mutant problem that historically blocked mutation testing from scaling. 73% engineer acceptance rate across 571 privacy-hardening tests applied to Facebook Feed, Instagram, Messenger, and WhatsApp. Published at FSE 2025.

### Formal verification as a practical gate

Amazon uses the Dafny verification-aware language to provide mathematical proofs of correctness for its Cedar authorization engine. A model is proved correct in Dafny, then agentic tools generate millions of inputs to ensure production Rust code matches the proven model — catching subtle design bugs that traditional testing missed. MIT's "vericoding" approach is also exploring LLMs' mathematical capabilities for producing code with proofs of correctness.

### The challenge

These examples are rare, and the fundamental difficulty is discovery. These techniques are by definition unpopular — most developers have never used formal verification, mutation testing, or LSTs, so you don't really know what to search for. The industry has much more energy going into adapting existing workflows to handle agent speed and volume than into rethinking what tools developers use. That means there's less activity, less writing, and fewer case studies in this space, which makes it hard to stumble onto the next interesting thread.

## Decision

Still exploring but struggling to find new threads to pull on. The mutation testing angle produced real projects, but the next interesting application of agents-enabling-new-paradigms is hard to find because there's just not a lot of activity or advancement happening in this area.

## References

- [Meta: LLMs Are the Key to Mutation Testing and Better Compliance](https://engineering.fb.com/2025/09/30/security/llms-are-the-key-to-mutation-testing-and-better-compliance/)
- [Meta: Revolutionizing Software Testing with LLM-Powered Bug Catchers](https://engineering.fb.com/2025/02/05/security/revolutionizing-software-testing-llm-powered-bug-catchers-meta-ach/)
- [Mutation-Guided LLM-based Test Generation at Meta (arxiv)](https://arxiv.org/abs/2501.12862)
- [Meta Applies Mutation Testing with LLM (InfoQ)](https://www.infoq.com/news/2026/01/meta-llm-mutation-testing/)
- [Lossless Semantic Trees (OpenRewrite docs)](https://docs.openrewrite.org/concepts-and-explanations/lossless-semantic-trees)
- [Open Source Auto-refactoring Meets AI Agent (Moderne/FINOS)](https://www.finos.org/blog/open-source-auto-refactoring-meets-ai-agent-to-modernize-fintech-software-at-scale)
- [How We Built Cedar with Automated Reasoning (Amazon)](https://amazon.science/blog/how-we-built-cedar-with-automated-reasoning-and-differential-testing)
- [mutation-test-gen](https://github.com/mathonsunday/mutation-test-gen) — my TypeScript mutation-guided test generator
- [go-mutation-test-gen](https://github.com/mathonsunday/go-mutation-test-gen) — my Go mutation-guided test generator with rapid integration
