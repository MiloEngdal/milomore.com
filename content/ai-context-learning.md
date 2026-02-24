---
title: "AI Context & Memory, Step by Step"
date: 2026-02-24T20:40:00+01:00
description: "A pedagogical guide to how context windows, memory, compaction, retrieval, and caching work in modern AI systems."
---

This page is a practical walkthrough of how modern AI systems manage context and memory.

If you have ever wondered why an assistant sometimes remembers details and sometimes forgets them, this is the map.

## 1. Start with the core distinction

Most confusion comes from mixing up two different things.

- **Context** is what the model can see right now in a single request.
- **Memory** is what the system can store and retrieve over time.

Think of context as a whiteboard. Think of memory as a library.

## 2. The context window is finite

Every model has a maximum context window measured in tokens.

When a conversation grows, the system must do at least one of these:

1. Drop old information
2. Summarize old information
3. Retrieve only relevant old information
4. Start a new session

This is not a bug. It is architecture.

## 3. What actually gets sent to a model

A production assistant prompt is usually layered like this:

1. System instructions
2. Developer rules
3. Tool schemas
4. Selected conversation history
5. Retrieved memory snippets
6. Current user message

Only this assembled package is in the live context for that turn.

## 4. Why costs rise over time

Token cost grows when:

- prompts include large repeated instructions
- history is long and not compacted
- tool outputs are massive
- retrieval is noisy and brings too much text

Latency often rises with the same drivers.

## 5. Compaction, explained simply

Compaction means: summarize older conversation into a compact entry and keep recent turns verbatim.

After compaction, future turns use:

- the summary of older history
- recent turns after the cutoff

Good compaction preserves decisions, constraints, and open questions.

## 6. Retrieval memory (RAG) in practice

Memory systems typically store notes in files or databases, then search them when needed.

A healthy retrieval pipeline does this:

1. Search for relevant snippets
2. Pull only small, high-signal chunks
3. Inject those chunks into context
4. Cite source when possible

Bad retrieval floods context and hurts quality.

## 7. Prompt caching and why it matters

Many requests share a stable prefix: same rules, same tools, same framing.

Prompt caching reuses processed prefixes.

Result:

- lower cost
- lower latency
- more predictable performance

Best practice: keep stable instructions at the top and variable user content later.

## 8. A 4-memory model you can teach

A useful teaching model is to separate four memory layers:

1. **Working memory**: current context window
2. **Session memory**: transcript history
3. **Semantic memory**: retrieval index and notes
4. **Policy memory**: rules and instruction files

Most systems are combinations of these four.

## 9. Platform examples

### ChatGPT

- Uses context window plus optional memory features
- Supports saved memory and history-based personalization
- Temporary chats reduce or bypass persistent memory usage

### Claude + Claude Code

- Large context options
- Prompt caching support
- File-based memory patterns like `CLAUDE.md` and project memory

### OpenAI Codex

- Project and user config layers
- Agent-oriented workflows with tools and approval/sandbox policies
- Supports compaction-oriented configuration

### OpenClaw

- Session transcripts in JSONL
- Manual and automatic compaction
- Workspace memory files with search/retrieval tools
- Skills and tools injected as part of runtime context

## 10. Where we are heading

The future is not just larger context windows.

The future is better orchestration:

- compact what is old
- retrieve what is relevant
- cache what is stable
- observe token spend continuously

In other words: context engineering becomes systems engineering.

## 11. Practical checklist for teams

Use this checklist when building your own assistant stack.

- Keep instruction prefixes stable
- Track token spend by layer (rules, history, tools, retrieval)
- Compact on thresholds, not panic
- Store durable facts in explicit memory
- Retrieve narrowly and cite sources
- Rotate sessions when scope changes
- Measure cache hit rate and compaction frequency

## 12. Suggested reading

- OpenAI Prompt Caching
- ChatGPT Memory FAQ
- Anthropic Prompt Caching
- Claude Code Memory docs
- OpenClaw docs on compaction and memory

---

If you want this transformed into a lecture deck, this page can be split into 10 slides almost directly.
