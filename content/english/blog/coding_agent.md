---
title: "Your AI coding agent is only as good as the codebase you give it"
meta_title: "Your AI coding agent is only as good as the codebase you give it"
description: "Article about architecture and language choices for LLMs"
date: 2026-03-18T05:00:00Z
image: "/images/posts/coding_agent/cover_image.jpg"
categories: ["Technology"]
author: "Rafal Koziarz"
tags: ["python", "java", "claude", "coding", "agent"]
draft: false
---

I've spent nearly 15 years building production systems — portfolio management, research and quant systems, enterprise financial technology across multiple geographies. The last three of those years have been with AI coding agents as a core part of the workflow. In that time I've seen the same pattern play out repeatedly: agents perform brilliantly on new projects and fall apart on large legacy ones. People blame the model. Usually they're wrong.

The real variable is the codebase itself — specifically two things: how explicitly your language forces contracts, and how cleanly your architecture separates concerns.

## Language is About Contracts, Not Syntax

The debate isn't really about which language is better. It's about how much a language forces you to be explicit. Languages that demand declared types, interfaces, return signatures and visibility modifiers give an AI agent something concrete to navigate by. When a method signature tells you exactly what goes in and what comes out, the model doesn't have to guess — and guessing is where it quietly goes wrong.

More flexible, expressive languages give the model more room. That room is useful for humans who can read intent and context. The model reads what's written. There's a meaningful difference between "easy for a human to read" and "hard for a machine to misinterpret," and in large codebases that gap compounds fast. A 2025 academic study found that 94% of LLM-generated compilation errors were type-check failures — which is another way of saying the type system was doing exactly the job of catching what the model got wrong.

There's a second factor worth naming alongside contracts: training data density. A language that's been written by millions of developers across billions of lines of publicly available code gives the model far more pattern recognition to draw from. A language with excellent contracts and strong safety guarantees but a fraction of the ecosystem representation means the model is navigating with good signage but less familiarity with the roads. The two don't always point in the same direction — on less common languages or frameworks you'll often see both problems at once, fewer constraints and less training signal to compensate. It's also worth acknowledging the nuance in the other direction: some loosely typed languages have such enormous training coverage that the model compensates reasonably well on small, self-contained tasks. It's on large, complex codebases where the lack of explicit contracts starts to hurt in ways that volume of training data can't fully paper over.

## Architecture Determines How Far the Agent Has to Look

A well-decomposed codebase with clear single responsibility keeps the relevant surface area per task small. The agent works within a bounded scope and gets it right. Tightly coupled code with tangled dependencies forces it to chase context across the entire system — and research is now fairly unambiguous that accuracy degrades sharply as context grows. One study documented accuracy drops of over 30% for information sitting in the middle of a long context window. More input is not the solution. Focused, relevant context consistently outperforms throwing everything at the model and hoping it finds what matters.

This isn't a new insight dressed up in AI terms. It's the same argument for good architecture that engineers have been making for decades — it just has a new and very concrete cost attached to it.

## There is a Way Forward for Legacy Systems

If you're sitting on a large legacy codebase, the answer isn't a full rewrite. It's identifying the modules your agents will touch most frequently and cleaning those up first — explicit types, clear boundaries, tight responsibility. Start there, not everywhere.

The irony is that the same agent that struggles with messy code is actually quite good at refactoring it incrementally — **provided you keep the scope small and maintain close oversight**. Pointed at a single, well-defined module with clear instructions, it can do solid work. Pointed at a tangled system and asked to sort it out, you're back to the original problem. The goal is to use it surgically: one module at a time, review everything, commit frequently. It won't transform a legacy system overnight but it makes the path forward less daunting than a ground-up rewrite.

## Where Senior Engineers Fit Into This — For Now

Bigger context windows and smarter models will help. But right now, this is where experienced engineers earn their place in an AI-augmented team in a way that's hard to replicate. When an agent produces garbage on a legacy system, someone has to diagnose which layer the problem lives at — the prompt, the model, the context, or the underlying architecture. That's a systems thinking problem, not a coding problem. Less experienced engineers and non-technical stakeholders tend to see "the AI isn't working" and either blame the tool or try a different model. A senior engineer knows which one to fix.

The sequencing decisions for incremental refactoring require the same depth. Knowing which dependencies are load-bearing versus historical accident, which modules are actually touched frequently versus which ones just look complicated — that's judgment that comes from time in the system, not from the agent itself.

That said, this is a "for now" argument more than a permanent one. As models improve and the tooling around them matures, what currently requires years of experience to diagnose will gradually become something any engineer on the team can work through. The diagnostic layer will get easier to navigate. What won't change as quickly is the deeper knowledge of the system itself — why certain decisions were made, what the business logic actually represents, where the real risk lives. That takes time in the domain, not just time with the tools.

Longer term, as models become more capable and context windows grow, some of this will matter less. But the economics won't disappear even if the technical constraints do — throwing compute at poor architecture is just expensive. The codebases that work best with AI agents are the ones that were already well-engineered. That's not a coincidence.

## Further Reading

- *Why AI is pushing developers toward typed languages* — GitHub Blog, January 2026 (includes the finding that 94% of LLM-generated compilation errors are type-check failures, and that TypeScript overtook Python and JavaScript as the most used language on GitHub in 2025)
- *Type-Constrained Code Generation with Language Models* — arXiv:2504.09246 — type-constrained decoding reduces compilation errors by more than half across models of various sizes
- *How Accurately Do Large Language Models Understand Code?* — arXiv:2504.04372 — 600K task study showing non-functional code changes reduce debugging accuracy by 78%

### Disclaimer

Co-written with Claude and image generated by Nano Banana Pro 2