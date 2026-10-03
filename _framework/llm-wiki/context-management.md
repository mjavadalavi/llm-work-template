# Context Management

## Problem
LLM context windows are finite and expensive. Every token of context costs:
1. Input tokens (money)
2. Processing time (latency)
3. Attention dilution (quality)

## Principles

### 1. Relevance Filtering
Only include what the agent needs for THIS specific task:
- Task description (always)
- Applicable §V invariants (always)
- Touched §I interfaces (always)
- File paths to modify (always)
- Prior feedback from review/test (if iterating)
- Related code snippets (only if non-obvious)

### 2. Progressive Disclosure
Don't load everything upfront. Agent reads:
1. Index first → find relevant pages
2. Drill into specific pages
3. Read code only for files it touches

### 3. Structured Over Unstructured
Pipe tables > prose paragraphs. §X.n addressing > "look at section 3 item 2".
Structured data = faster parsing = fewer tokens = less ambiguity.

### 4. Persistent State Over Context
Instead of repeating info in every agent prompt:
- Write to SPEC.md (persists across agents)
- Write to llm-wiki/ (persists across sessions)
- Write to docs/ (persists across phases)
- Reference file paths instead of inlining content

### 5. Output Compression
Agent output should be:
- Structured (tables, lists, §X.n refs)
- Caveman-encoded for spec docs
- No redundant preamble/postamble
- Code in fenced blocks, not inline

## Context Pack Template
When spawning a subagent:
```
## Task
<one paragraph what to do>

## Constraints
- §V.1: <invariant>
- §V.3: <invariant>

## Interfaces
- §I.api: POST /x → 200 {id}

## Files
- Create: src/handlers/x.ts
- Edit: src/routes.ts

## Feedback (if iterating)
- Review: <specific issues>
- Test: <specific failures>
```

## Anti-Patterns
- Pasting entire files into prompt
- Repeating SPEC.md contents (just reference it)
- Including irrelevant history
- Verbose instructions when skill file covers it
- Multiple agents reading same large file (use summary)

## Sources
- RTK philosophy: "filter before it reaches context"
- Cavekit: "spec loaded every invocation → must be small"
- Ralph: "fresh context → must be self-contained but minimal"
