# Model Tier Selection

## Principle
Different tasks benefit from different model capabilities. Using a high-reasoning model for simple code generation wastes money. Using a fast model for architecture planning produces poor results.

## Tier Definitions

### High (Reasoning)
- Models: qwen3.7-max, qwen3.7-plus
- Strengths: Complex reasoning, multi-step planning, architectural decisions, ambiguity resolution
- Cost: High per token
- Use for: Clarification, architecture, orchestration decisions

### Mid (Analysis)
- Models: glm-5.1, qwen3.7-plus
- Strengths: Thorough analysis, pattern recognition, balanced speed/quality
- Cost: Moderate
- Use for: Code review, test design, architecture review, task decomposition

### Fast (Throughput)
- Models: deepseek-v4-flash, minimax-m3
- Strengths: High throughput, code generation, mechanical tasks
- Cost: Low per token
- Use for: Implementation, code formatting, simple edits

## Assignment Matrix

| Agent | Tier | Rationale |
|-------|------|-----------|
| clarifier | High | Must resolve ambiguity, infer requirements |
| researcher | High + web | Must synthesize diverse sources |
| architect | High | Complex system design, multi-milestone planning |
| arch-reviewer | Mid | Analysis of existing designs, not creation |
| orchestrator | High | Coordination decisions, escalation judgment |
| implement | Fast | High-volume code generation |
| reviewer | Mid | Thorough analysis, not creative work |
| tester | Mid | Test design requires thought, not speed |
| taskman | Mid | Task decomposition is structured analysis |

## Dynamic Selection (Future)
Could route by:
- Task complexity (simple fix → fast, new feature → high)
- File count (1 file → fast, 10 files → mid)
- Review severity (minor → fast re-fix, major → high re-architect)

## Cost Optimization
- Batch similar tasks (implement all simple tasks with fast model)
- Use high model only for decisions, not execution
- Cache/spec persistent state to avoid re-derivation

## Sources
- Current agent definitions (model fields in frontmatter)
- General LLM deployment patterns
