---
title: "From Weekend Coding to Context Engineering: A Professional Development Journey"
meta_title: "Context Engineering"
description: "Moving beyond prompt engineering to building real systems"
date: 2025-07-20T05:00:00Z
image: "/images/posts/context_engineering_2.png"
categories: ["Technology"]
author: "Rafal Koziarz"
tags: ["artifical intelligence", "development"]
draft: false
---

## Why I Haven't Written in a While

In my [last post about Home Lab](/blog/home_lab/), I promised a Part 2 covering agent swarms, automation workflows, and exposing services to the internet. That was back when I was doing hobby coding with Cursor, experimenting with prompt engineering, and exploring AI possibilities in my spare time.

Then I started a new company.

Suddenly, exploratory coding turned into building production systems for real clients. The playful experimentation with LLMs became the foundation for enterprise-grade AI solutions. And honestly? It's been a tough journey. Moving from hobby "vibe coding" with Cursor to architecting reliable AI systems forced me to rethink everything I thought I knew about working with AI.

This post is about that journey—and how I accidentally discovered that the key to professional AI development isn't better prompts, it's better context engineering.

## The Reality Check

When you're building systems that clients depend on, the casual prompt engineering approach falls apart quickly. You can't have an AI agent that works 80% of the time and fails mysteriously the other 20%. You need reliability, consistency, and the ability to understand why something went wrong.

My first few months were humbling. The same techniques that felt magical in hobby projects with tools like Cursor—clever prompts, creative workarounds, hoping the AI would "figure it out"—became liabilities when building real products.

For professional work, I moved to Claude Code with the pro plan, which I believe is currently the best coding agent available. The reliability and context handling capabilities are essential when client work depends on consistent AI performance.

The turning point came when I realized I was approaching this backwards. Instead of trying to write perfect prompts, I needed to architect the information environment the AI operates in.

## Information Architecture Meets AI

Coming from a systems background, I started thinking about AI context the same way I'd think about any information architecture problem:

**The Core Questions:**
- How do humans manage cognitive load effectively?
- What information do they need, when do they need it, and in what format?
- How do you provide just enough context without overwhelming the system?

**Applied to AI:**
- Structure knowledge so AI can navigate it systematically
- Provide context dynamically based on the current task
- Build systems that can expand context when needed, not dump everything upfront

This shift from "prompt engineering" to "context engineering" changed everything.

## Building Context Systems That Actually Work

### The Technical Approach

For our development team (human + AI agents), I built a context system around:

**Structured Knowledge Base**
```
├── Product vision (markdown in monorepo)
├── Feature specifications (Linear integration)
├── Architecture decisions (living documentation)
└── Implementation history (git + documentation)
```

**Dynamic Context Assembly**
- Agents start with minimal, task-relevant context
- They can request additional information as needed
- Context is assembled from multiple sources (Linear, docs, codebase)
- Human-in-the-loop for quality gates

**Real Example - Feature Request Flow:**
1. "Add user authentication to dashboard"
2. Agent scans existing auth architecture
3. Agent finds related Linear stories
4. Agent identifies reusable components
5. Agent provides contextualized response: "You have OAuth already built, this connects to Epic AUTH-001, recommend extending UserService class"

Instead of starting from scratch, we get development plans that build on existing work.

### The Information Architecture Principles

**Hierarchical Context**
- Summary level: What exists and how it relates
- Detail level: Specific implementation notes
- Deep dive: Full technical specifications

**Just-in-Time Information**
- Agents get basic context initially
- They can traverse the knowledge graph for more details
- Context window stays manageable

**Bidirectional Learning**
- Agents can suggest when documentation is outdated
- They identify gaps in context during task execution
- The system improves through use

## Working with Existing Codebases

The real test of context engineering came when working with client codebases—often poorly documented, legacy systems where institutional knowledge lived only in people's heads.

**The Challenge:**
- Codebases with minimal documentation
- Business logic scattered across multiple files
- No clear relationship between features and requirements
- Previous developers long gone

**Context Engineering Solution:**
We built agents that could analyze existing code and retrospectively create context:

- **Reverse Documentation:** Agents scan code patterns and generate architecture documentation
- **Feature Mapping:** Connect code components to business functionality  
- **Decision Archaeology:** Infer why certain technical decisions were made based on code structure

**Unexpected Byproducts:**
The context engineering process generated useful artifacts beyond just AI context:
- **User Documentation:** Clear explanations of what the system actually does
- **Technical Documentation:** Architecture diagrams and component relationships
- **Release Notes:** Meaningful descriptions of changes based on code analysis and story context

Instead of manually documenting everything upfront, the context system builds documentation as a natural byproduct of understanding the codebase for development work.

## What I Learned About Professional AI Development

### Context Failures vs. Model Failures

Most AI agent failures in production aren't because the model is bad—they're because the agent lacks sufficient context to make good decisions. When you architect context properly, even simpler models can perform reliably.

### Human-AI Collaboration Patterns

The goal isn't fully autonomous AI. It's AI that can work independently on well-defined tasks but knows when to involve humans for important decisions.

Our quality gates:
- **Auto-approve:** Documentation updates, simple bug fixes
- **Human review:** New features, architecture changes
- **Human required:** Product decisions, user-facing changes

### Evolutionary Development

Context engineering isn't something you design once and deploy. It's a constantly evolving system that improves through use. Agents identify context gaps, suggest documentation improvements, and help refine the information architecture over time.

## Technical Implementation

## Why I Chose Linear

After evaluating project management tools, Linear won me over with [their methodology](https://linear.app/method). They focus on "building true quality software" with foundational practices that align perfectly with structured development.

What really sold me was their systematic approach to breaking down work and maintaining development momentum. Plus, Linear now has a native MCP server, which means LLMs can interact with it more naturally—accessing issues, updating status, and understanding project context without custom API integration.

## Linear → Development Workflow

Our development process revolves around Linear's structured approach:

**Story Creation and Breakdown:**
- Features start as high-level stories in Linear
- Context engineering helps determine if a story is "too big"
- We break down stories until they fit within manageable context windows
- Each story becomes a git branch with clear scope

**Development Flow:**
1. **Story Selection:** Pick story from Linear backlog
2. **Context Assembly:** Agent gathers related documentation, previous implementations, technical constraints
3. **Branch Creation:** Story-specific branch with focused scope
4. **Task Offloading:** Break story into temporary working files so AI can resume work without losing context
5. **Implementation:** Development with full context of requirements and existing codebase
6. **Review and Merge:** Human review of changes against story requirements

**Process Evolution:**
This workflow helps us continuously refine what works:
- **Context Testing:** Each story becomes an experiment in what context is needed
- **Story Sizing:** Learn what constitutes a "too big" story that should be broken down
- **Context Optimization:** Discover which information sources are most valuable for different types of work

The git branch structure gives us natural checkpoints to evaluate context effectiveness and iterate on our approach.

### Context Assembly Pipeline

1. Parse task for keywords and intent
2. Query structured data (Linear) for related items
3. Search unstructured knowledge (markdown, vector similarity)
4. Assemble hierarchical context (summary → details → specifics)
5. Optimize for token limits
6. Present to agent with expansion capabilities

## Lessons from Building Production Systems

### What Works

**Structured Knowledge Beats Clever Prompts**
Instead of perfecting how you ask questions, focus on what information the AI has access to when answering.

**Context Reusability**
Well-structured context gets reused across different tasks. Good architecture documentation becomes valuable context for feature development, bug fixes, and onboarding.

**Feedback Loops**
Agents can suggest context improvements: "This document seems outdated" or "I needed additional information about X to complete this task."

### What Doesn't Work

**Over-Engineering Early**
Don't try to create comprehensive context for every scenario upfront. Start focused, expand based on actual needs.

**Static Documents**
Long, static documents become outdated quickly. Prefer smaller, interconnected pieces that stay current through regular use.

**Ignoring Human Factors**
Optimize for human-AI collaboration, not AI autonomy. Humans need to understand and maintain these systems.

## Moving Forward

The shift from hobby coding to professional AI development has been challenging but rewarding. Context engineering emerged naturally from the need to build reliable systems that clients can depend on.

This approach scales—from our two-person team to enterprise clients with complex requirements. The core insight remains: most AI failures are context failures, and treating context as an engineering discipline changes how you build with AI.

I'll eventually share more use cases and user stories on our [company website](https://cohort.hk) as we continue developing these approaches with clients.

---

*Yes, I still owe you that Home Lab Part 2 post. Maybe after I figure out how to scale context engineering to handle my growing pile of unfinished blog posts.*

## Notes

**Info**
Context engineering is designing systems that provide AI models with the right information, in the right format, at the right time to accomplish tasks effectively.

**Info**  
Linear is a project management tool that provides structured context through its API—perfect for giving AI agents access to organized project information.

**Note**
I typically try to avoid using AI to help write my blog posts, but with limited time and wanting to get these valuable insights out there, Claude helped me structure and refine this post based on my experiences and notes.