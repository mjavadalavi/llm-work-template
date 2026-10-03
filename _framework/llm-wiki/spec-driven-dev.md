# Spec-Driven Development

## Core Idea
Plan-then-execute forgets. Spec-driven development (SDD) remembers.

The spec is a **persistent, compounding artifact** that survives context resets. Unlike plans that get discarded after execution, the spec accumulates knowledge: invariants learned from bugs, interfaces refined over time, tasks tracked to completion.

## Key Principles

### 1. Single Source of Truth
One file (SPEC.md) at repo root. All agents read it. Only designated commands mutate it. No scattered state files, no dashboards, no parallel tracking.

### 2. Addressable Sections
Fixed sections with `§X.n` addressing:
- §G Goal, §C Constraints, §I Interfaces, §V Invariants, §T Tasks, §B Bugs
- Commits, PRs, commands all reference by §. Zero ambiguity.

### 3. Backprop Protocol
Every bug → §B entry + usually new §V invariant. The spec **learns** from mistakes. Recurrence of a bug class becomes impossible because the invariant catches it.

### 4. Caveman Encoding
Spec loaded every invocation. ~75% fewer tokens via compressed encoding: drop articles, use symbols, fragments OK. Preserves code/paths/identifiers verbatim.

### 5. Minimal Ceremony
No sub-agents for spec management. No dashboards. `cat SPEC.md` is the dashboard. One file rule: big projects get more sections, not more files.

## Sources
- Cavekit v4 (JuliusBrussee/cavekit): SPEC.md format, caveman encoding, backprop
- Comparison: v3 had 16 commands + 12 sub-agents → v4 has 3 commands + 0 sub-agents
- Philosophy: "The spec is the only artifact that earns its tokens"

## Cross-References
- → [caveman-encoding](caveman-encoding.md) for encoding rules
- → [autonomous-loop](autonomous-loop.md) for how Ralph uses similar patterns (PRD + progress)
- → [agent-orchestration](agent-orchestration.md) for how SDD integrates with multi-agent systems
