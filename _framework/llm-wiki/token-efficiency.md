# Token Efficiency

## Problem
LLM agent systems consume tokens on every roundtrip. Costs compound with: verbose prompts, redundant context, unnecessary roundtrips, unfiltered command output.

## Strategies

### 1. Caveman Encoding (~75% savings)
Compressed language for spec/plan docs. Drop articles, filler, aux verbs. Use symbols. See [caveman-encoding](caveman-encoding.md).

### 2. Command Output Filtering (60-90% savings)
RTK proxy: intercepts CLI commands, filters output before it reaches LLM context. Flag-aware: default = aggressive compression, verbose flags = pass-through.
See [rtk-proxy](rtk-proxy.md).

### 3. Minimal Context Packing
Each agent gets only what it needs:
- Specific task description
- Relevant §V invariants
- Relevant §I interfaces
- File paths it touches
- Prior review/test feedback

Never dump entire codebase or all docs.

### 4. Model Tier Selection
| Task | Tier | Why |
|------|------|-----|
| Complex reasoning/planning | High (qwen3.7-max) | Quality > speed |
| Code generation | Fast (deepseek-v4-flash) | Throughput > depth |
| Review/analysis | Mid (glm-5.1) | Balanced |

### 5. Reduce Roundtrips
- Give agents everything they need in one shot
- Use structured output formats (pipe tables, §X.n addressing)
- Pre-compute cross-references (don't make agent search)
- Batch independent operations

### 6. Persistent State Over Re-derivation
- SPEC.md survives context resets
- llm-wiki accumulates knowledge
- progress.txt/logs prevent repeated work
- Pattern consolidation avoids repeated mistakes

### 7. Early Termination
- ComposedPhases with break conditions
- Stop iterating when quality gate passes
- Don't re-review code that already passed

## Metrics
- Token savings target: 60-90% on command output
- Spec encoding savings: ~75% vs prose
- Context packing: O(task-relevant) not O(everything)

## Sources
- RTK (rtk-ai/rtk): command proxy architecture
- Cavekit (caveman encoding)
- General LLM optimization patterns
