# Agents.md Best Practices

## Key Data Points
- Auto-generated AGENTS.md → -3% success, +20% cost (ETH Zurich 2025)
- Human-written → +4% success, +19% cost (still wasteful)
- Codebase overviews don't help navigation speed
- Tools mentioned in AGENTS.md used 160x more than unmentioned
- Instruction budget: ~150-200 instructions max (agent harness uses ~50)
- Unnecessary requirements → +14-22% reasoning tokens

## What to Include
- **WHAT**: tech stack, project structure, what each part does
- **WHY**: purpose, intent behind components
- **HOW**: build, test, verify. Non-obvious tooling (uv not pip, bun not npm)

## What NOT to Include
- Detailed directory listings (agents discover structure themselves)
- Code style guidelines (use linters instead — deterministic, cheaper)
- Task-specific instructions that don't apply universally
- Auto-generated content (/init hurts more than helps)

## Structure Rules
- **< 150 lines** (HumanLayer keeps < 60). Every line goes into every session.
- **Progressive disclosure**: separate files for task-specific docs, list in AGENTS.md with brief descriptions
- **Pointers > copies**: reference file:line, don't embed code that goes stale
- **Write deliberately**: bad line cascades into bad plans/code across all sessions

## Three-Tier Boundaries
- **Always do**: run tests before commits, follow naming conventions
- **Ask first**: DB schema changes, adding dependencies
- **Never do**: commit secrets, edit node_modules/, modify CI config

## Six Core Areas (GitHub study of 2500+ repos)
1. Commands (with full flags: `npm test`, `pytest -v`)
2. Testing (framework, locations, coverage expectations)
3. Project structure (src/, tests/, docs/)
4. Code style (one real snippet > three paragraphs)
5. Git workflow (branch naming, commit format, PR requirements)
6. Boundaries (never touch: secrets, vendor/, production configs)

## Cross-Tool Compatibility
- AGENTS.md = master file (OpenCode, Cursor, Copilot read natively)
- GEMINI.md → `@AGENTS.md` hook
- CLAUDE.md → `@AGENTS.md` hook or symlink
- .github/copilot-instructions.md → reference link
- Nested AGENTS.md in subdirs for monorepos (nearest wins)

## Anti-Patterns
- Vague prompts ("build something cool")
- Overlong contexts without summarization
- Skipping human review
- Auto-generating with /init
- Letting it become outdated (stale docs poison context)
- Single AGENTS.md for large monorepos

## Sources
- agents-md-guide.md, writing-good-agents-md-file.md, agents-md-file-to-rule-them-all.md, complete-agents-md-file-guide.md, agents-md-website.md
