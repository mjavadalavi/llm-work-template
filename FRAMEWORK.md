## Top-level structure

- ./repo is a public code repo.
- ./llm-wiki is where you would gather your knowledge.
- ./_framework/llm-wiki is where other read-only framework knowledge has been gathered. 
- ./_sources are sources for inspiration and knowledge gathering.

**Remember**: Never mention things outside ./repo inside of it, unless they are publicly available (things that are available in _sources) but without mentioning our private structure.

## Git work style

Your work will be in atomic commits (commits that don't break things and are atomic: can't be split), and with short messages like: "xxxx: yyyy" such as "chore: update README.md", but with long description as always.

Project public documentation will be in ./repo/docs, and will be summaries about architecture, design decisions, how to use each feature, how to interact with this project, how it can be setup and deployed, and other things that have their place in every production-ready project's docs.

## Highest level requirements

### If project is going to have a CLI

Project must be easy to setup for beginner users, have JSONL mode for input/output on console (in non-interactive mode) while human-readable input/output on console should be default and TUI should be provided as an alternative, with wizard for config in all modes, while config could be written by hand in YAML and also done through non-interactive CLI flags. CLI commands may be well structured, but root command will be "init on first run, or main command when configured"

So CLI will have these modes:

- non-interactive
  - everything via CLI flags
  - output format in JSONL or human-friendly (default)
- interactive
  - JSONL: for GUI wrappers
  - lite: human-friendly
  - full: TUI experience (default)

### If project is going to have a library

It will be structured as the way that is idiomatic for that ecosystem/language. For example, JS/TS projects have their own structure which should not be used in Go projects.

### If project is going to have a protocol/wire format/file format

Document it well for other projects to be able to use it in even different programming languages.

## How to execute

- First read framework's llm-wiki topics. You will abide by them and this document.
- Then finalize requirements
- Research if required by user, or if you need knowledge about things from "_sources".
- Then capture knowledge in llm-wiki
- Then do the architecture
- After architecture finalization, write on implementation stack and style.
- Write Plans milestone-based consisting of small steps, with clear set of deliverables and release points (with publish and versioning in mind) marked.
- Then execute.
  - user may give you new considerations during tasks. do not execute them right there. instead, put them into a backlog, then readjust architecture and design for them, then the planning, then continue your work from where you stopped.
  - Use your tools such as todo/task lists to manage work on smaller steps.
  - Mark your progress in the planning docs of llm-wiki.

## Code style

- Make sure to write highly-efficient parallelizable code being lock-free as possible and using high-performance backends, while not sacrificing code reusability, quality and other things.
- Code must be idiomatic to that language.
- Use battle-tested libraries and packages when possible. Not every scenario needs to reinvent the wheel, unless said by the user.

## Responses in conversation

Talk less, but effective. Remove verbs when not necessary. Short summaries suffice. Short sentences are usually better. When suitable, use arrows (or even better, unicode arrows) for shorter talk like "M1 -> done. Commit -> done" instead of "The work on Milestone M1 has been done with clear set of deliverables being successfully tested, did an atomic commit afterwards".