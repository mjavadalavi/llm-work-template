# Agent Orchestration Patterns

## Pattern 1: Sequential Pipeline
```
clarify → research → architect → review → build
```
Each phase produces artifacts consumed by next. Linear, predictable.

## Pattern 2: Build Loop (Sprint)
```
for task in tasks:
  implement → review → [fix] → test → [fix] → done
```
Inner loop with quality gates. Iterate until pass or escalate.

## Pattern 3: Role-Playing (AgileCoder)
Two agents in structured conversation. Assistant + User roles. Ends on `<INFO>` marker or turn limit. Self-reflection if no conclusion.

## Pattern 4: Fresh Instance Loop (Ralph)
Spawn fresh agent per task. Clean context. Memory via files (PRD, progress.txt, CLAUDE.md). Avoids context pollution.

## Pattern 5: ComposedPhase with Early Break
Loop of sub-phases. Break when:
- Reviewer says "Finished"
- No bugs found in test
- All items pass quality gate

## Our Framework's Hybrid
Combines patterns 1, 2, 4, 5:
1. Sequential pipeline for phases 1-4 (clarify → research → plan → review)
2. Fresh instance per subagent (pattern 4)
3. Build loop per task (pattern 2)
4. Early break on quality gates (pattern 5)

## Orchestration Rules
1. Orchestrator never implements. It delegates.
2. Each subagent gets minimal context (context packing).
3. Quality gates between steps: review after implement, test after review.
4. Escalation path: if fix fails twice → stop and report to user.
5. Log everything to llm-wiki/log.md.

## Anti-Patterns
- **Context dumping**: giving agent entire codebase
- **Infinite loops**: no max iteration count on build loop
- **Skipping gates**: going implement → done without review/test
- **Shared mutable state**: agents editing same files concurrently
- **Over-decomposition**: splitting tasks so small overhead > work

## Sources
- AgileCoder: ChatChain + ComposedPhase patterns
- Ralph: fresh instance loop
- Cavekit: minimal ceremony, single-thread
