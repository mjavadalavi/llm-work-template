# Skill Writing for Agent Systems

## Core Principle

A skill is a reusable instruction bundle discovered and loaded on demand. The `description` is the only routing metadata — it decides whether the skill loads. The body teaches a procedure.

## Description Is the Routing Key

The agent sees only `name` and `description` before loading the skill body. Every other word is invisible until triggered.

- **Bad**: "Helps with testing" — too vague, triggers for anything
- **Good**: "Generate test cases for API handlers using table-driven patterns" — specific action + context
- **Best**: Write for agent selection, not for humans. Include trigger keywords (what user says when frustrated).
- **Length**: 1–1024 characters. Be specific, not generic.
- **Test**: Does the skill trigger for the right prompts and NOT trigger for wrong ones?

## Progressive Disclosure Hierarchy

Skills load in layers:

| Layer | What | Token Cost |
|-------|------|------------|
| 1. Metadata | `name` + `description` only | ~100 tokens/skill |
| 2. Instructions | Full SKILL.md body | ~500 lines max |
| 3. Resources | Reference files, scripts, templates | Loaded only when referenced |

## Body Structure

A well-structured SKILL.md follows this pattern:

1. **Goal** — what the skill accomplishes (1-2 lines)
2. **When to use** — triggers and context
3. **Workflow** — step-by-step numbered procedure
4. **Decision rules** — if/then branches
5. **Gotchas** — negative examples, what NOT to do
6. **Validation** — how to verify the result is correct
7. **Output format** — what to produce
8. **References** — files to consult (JIT loaded)

## Content Guidelines

### Do
- Use step-by-step numbering — agents pattern-match on sequential workflows
- Provide concrete examples — before/after, templates, expected output
- Use pipe tables for structured data — faster to parse than prose
- Say what TO DO, not what NOT to do (exception: gotchas section)
- Use third-person imperative: "Extract the text..." not "You should..."
- Include verification steps — let agent self-check its work
- Flat reference structure — files one level deep, no nested chains
- Use relative paths with forward slashes

### Don't
- Dump every command someone needs to run (readme style = garbage skill)
- Exceed ~500 lines in SKILL.md
- Include auto-generated content — stale docs poison context
- Write vague descriptions — imprecise routing kills discoverability
- Skip the gotchas section — highest signal-to-noise content
- Nest reference files more than one level deep

## Gotchas Are High-Value Content

Negative examples teach the agent what to avoid. Start thin and grow organically: every time the agent trips up on the skill, add a gotcha line.

Examples:
- "Never modify `node_modules/`"
- "Do NOT commit generated files alongside source — separate PR"
- "If the API returns 429, wait 5s and retry, don't abort"

## Three-Tier Boundaries in Skills

| Tier | Effect | Example |
|------|--------|---------|
| Always do | Required step | "Run tests before committing" |
| Ask first | Pause for confirmation | "Ask user before deleting branches" |
| Never do | Blocked | "Never modify CI config files" |

## Test Before Writing

Run the task without a skill first. If the agent already performs well, you don't need a skill. If it struggles, a skill adds value. Write eval prompts (positive + negative cases) to verify the skill triggers correctly.

## Cross-Platform Compatibility

Skills defined with `name` + `description` in YAML frontmatter work across:
- OpenCode (`.opencode/skills/<name>/SKILL.md`)
- Claude Code (`.claude/skills/<name>/SKILL.md`)
- Cursor, Gemini CLI (standard SKILL.md format)

## Our Framework's Skill System

Our skills are defined as YAML in `pkg/assets/template/skills-defs/` with two content fields:
- `content` — human-readable (pedagogical, teaches the concept)
- `cavemanized` — token-compressed (for agent use in tight context)

The generation tool (`cmd/gen-skills/`) produces `.md` files with frontmatter. Mode flag selects which content field to use. Version overrides allow per-skill variant selection (e.g., `caveman@original.yaml`).

Skills are for target projects using the framework, not framework development itself. They fall into two categories:
1. **Generalized best practices** — language/framework-agnostic workflows (build, testing, deploy-config, release, problem-solving, code-generators)
2. **Framework-tool skills** — how to use agent-facing framework tools (analytics, ask, backprop, caveman, mcp, etc.)

## Sources
- Claude API Docs: Skill authoring best practices (platform.claude.com)
- Perplexity Research: Designing, Refining, and Maintaining Agent Skills
- mgechev/skills-best-practices (GitHub)
- OpenCode Agent Skills Guide (opencodeguide.com)
- Lalit Madan: The SKILL.md Guide
- Addy Osmani: How to write a good spec for AI agents
- Our framework: prompt-engineering.md, agents-md-best-practices.md, spec-writing-for-agents.md

## Cross-References
- → [prompt-engineering](prompt-engineering.md) for prompt-level design
- → [agents-md-best-practices](agents-md-best-practices.md) for AGENTS.md (not skill) writing
- → [spec-writing-for-agents](spec-writing-for-agents.md) for spec writing patterns
- → [context-management](context-management.md) for progressive disclosure and JIT loading
