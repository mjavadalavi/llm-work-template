# Autonomous Agent Loop (Ralph)

## What
Bash loop that spawns fresh AI instances repeatedly until all PRD items complete. Each iteration = clean context.

## Core Pattern
```
while stories remain:
  1. Fresh AI instance (clean context)
  2. Read PRD (prd.json)
  3. Read progress.txt (Codebase Patterns section first)
  4. Check branch
  5. Pick highest priority story where passes=false
  6. Implement that story
  7. Run quality checks (typecheck, lint, test)
  8. If pass → commit + update PRD + append progress
  9. If all pass → COMPLETE
```

## Memory Persistence
Since each iteration has clean context, memory persists via:
1. **Git history** — code changes, commits
2. **progress.txt** — what was done, learnings, patterns
3. **prd.json** — story status (passes: true/false)
4. **CLAUDE.md files** — reusable patterns per directory

## Progress Report Format
```
## [Date/Time] - [Story ID]
- What was implemented
- Files changed
- **Learnings for future iterations:**
  - Patterns discovered
  - Gotchas encountered
  - Useful context
---
```

## Codebase Patterns
Consolidated at TOP of progress.txt. General, reusable learnings:
- API patterns specific to module
- Gotchas for file relationships
- Testing approaches per area
- Configuration requirements

## CLAUDE.md Updates
Before commit, check if edited files have learnings worth preserving in nearby CLAUDE.md files. Only genuinely reusable knowledge. Not story-specific details.

## Key Design Decisions
1. **Fresh instances** — avoids context pollution, each starts clean
2. **One story per iteration** — focused, minimal scope
3. **PRD as state** — machine-readable, tracks completion
4. **Pattern consolidation** — learnings accumulate, prevent repeated mistakes
5. **Stop condition** — explicit `<promise>COMPLETE</promise>` when all done

## Lessons for Our Framework
- Fresh context per agent → our subagent spawning model
- Progress logging → our llm-wiki/log.md
- Pattern consolidation → our llm-wiki knowledge entries
- PRD as state → our SPEC.md §T task tracking
- Quality gates → our review + test steps in build loop
- One task per iteration → our per-task build loop

## Source
- rtk-ai/ralph (CLAUDE.md, prd.json.example)
