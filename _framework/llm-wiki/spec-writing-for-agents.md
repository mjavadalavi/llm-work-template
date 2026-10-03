# Spec Writing for AI Agents

## Core Principle (Addy Osmani)
Aim for clear spec covering **just enough nuance** to guide without overwhelming. Break large tasks into smaller ones. Plan first in read-only mode, then execute and iterate.

## Five Principles

### 1. Start High-Level, Let AI Draft Details
- Concise goal statement + core requirements → agent generates detailed spec
- Use Plan Mode (read-only) for planning phase before execution
- Spec becomes persistent reference between sessions
- Focus on what/why, not nitty-gritty how (initially)

### 2. Structure Like Professional PRD/SRS
Six core areas: Commands, Testing, Project structure, Code style, Git workflow, Boundaries

**GitHub Spec Kit four-phase workflow:**
1. **Specify** — high-level description, user journeys, success criteria
2. **Plan** — technical stack, architecture, constraints
3. **Tasks** — small, reviewable, isolatable chunks
4. **Implement** — one task at a time, verify at each phase

### 3. Modular Prompts, Not One Big Prompt
- "Curse of instructions" — more instructions → worse adherence to each
- Divide spec into phases/components, feed only relevant slice per task
- Extended TOC with summaries: bird's-eye view stays in prompt, details loaded on demand
- Sub-agents per spec area: each has smaller context, focused role
- One task focus + relevant info only per prompt

### 4. Self-Checks, Constraints, Human Expertise
- **Three-tier boundaries**: Always / Ask first / Never
- Encourage self-verification: "compare result with spec, confirm all requirements met"
- LLM-as-Judge for subjective checks (style, readability, patterns)
- Conformance testing: language-independent tests derived from spec
- Domain knowledge: encode pitfalls, preferences, style guidelines
- Adjust spec detail to task complexity

### 5. Test, Iterate, Evolve
- Continuous testing after each milestone/function
- Iterate on spec itself when incomplete/unclear
- Context-management tools: RAG, MCP, hierarchical summaries
- Parallelize carefully: ensure tasks truly independent
- Version control spec like code
- Cost/speed: cheaper model for drafts, expensive for reasoning
- Monitor and log everything

## Anti-Patterns
- Vague prompts → wrong results
- Overlong contexts without summarization
- Skipping human review
- Conflating vibe coding with production engineering
- "Lethal trifecta": speed + non-determinism + cost → cut corners on verification
- Missing six core areas

## Source
- good-spec-for-ai-agent.md (Addy Osmani)
- best-practices.md (Jonathan Vila)
- best-practices2.md (Reddit)
- sample-agents-md-file.md
