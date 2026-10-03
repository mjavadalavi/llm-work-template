# Agent Architecture Patterns

## Anthropic's Building Effective Agents
- **Workflows** = predefined code paths; **Agents** = LLMs dynamically direct own processes
- Start simple, add complexity only when needed
- Frameworks add abstraction that obscures debugging

### Workflow Patterns
1. **Prompt chaining** — sequential steps with programmatic gates
2. **Routing** — classify input, direct to specialized followup
3. **Parallelization** — sectioning (independent subtasks) + voting (multiple attempts)
4. **Orchestrator-workers** — central LLM dynamically delegates to workers
5. **Evaluator-optimizer** — one generates, another evaluates in loop

### Three Core Principles
1. Maintain simplicity
2. Prioritize transparency
3. Craft agent-computer interfaces (ACI) — tool formats matter, give thinking tokens

## Components of a Coding Agent (Sebastian Raschka)
1. **Live Repo Context** — workspace summary built upfront (git branch, AGENTS.md, layout)
2. **Prompt Shape & Cache Reuse** — stable prefix (instructions, tools, summary) cached; only transcript/request changes per turn
3. **Tool Access** — pre-defined named tools with validation, approval gating, path restrictions
4. **Minimizing Context Bloat** — clip long outputs, reduce transcript, deduplicate file reads, recency-weighted compression
5. **Structured Session Memory** — working memory (distilled state) + full transcript (durable JSON)
6. **Delegation with Bounded Subagents** — parallelize into subtasks; subagents inherit context but constrained (read-only, limited recursion)

## Deep Agents (LangChain)
- **Subagents**: context isolation, prevent "dumb zone" (context rot)
- **Skills**: progressive disclosure — descriptions pre-loaded, body loaded only when needed
- General-purpose subagent: mirrors main agent, perfect for context isolation without specialization

## Single vs Multi-Agent
| Factor | Single | Multi |
|--------|--------|-------|
| Best for | Tightly coupled, short tasks | Open-ended, parallelizable |
| Context | Easy — one agent maintains state | Hard — must shard across agents |
| Reliability | Consistent, fewer failure modes | Can fail if orchestration brittle |
| Cost | Lower | Higher (parallel calls) |

## Key Insight
Multi-agent research system (Opus 4 lead + Sonnet 4 subagents) outperformed single Opus 4 by 90.2% on research tasks. Token usage explained 80% of performance variance.

## Sources
- building-effective-agents.md (Anthropic)
- components-of-coding-agent.md (Raschka)
- multi-agent-deep-agents.md (LangChain)
- llm-agent-build-guide.md (Vellum)
