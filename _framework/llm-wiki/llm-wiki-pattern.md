# LLM Wiki Pattern

## What
Instead of RAG (re-deriving knowledge every query), LLM incrementally builds and maintains a persistent wiki — structured, interlinked markdown files.

## Three Layers
1. **Raw sources** — immutable curated documents. LLM reads, never modifies.
2. **The wiki** — LLM-generated markdown. Summaries, entities, concepts, cross-references. LLM owns entirely.
3. **The schema** — config file (CLAUDE.md / AGENTS.md) telling LLM how wiki is structured, conventions, workflows.

## Operations

### Ingest
New source → LLM reads → writes summary → updates index → updates relevant entity/concept pages → appends log entry. Single source may touch 10-15 pages.

### Query
Ask question → LLM searches wiki → reads relevant pages → synthesizes answer with citations. Good answers filed back as new pages. Explorations compound.

### Lint
Health-check: contradictions, stale claims, orphan pages, missing cross-references, concepts without pages, data gaps.

## Key Files
- **index.md** — content-oriented catalog. Each page + link + one-line summary. By category. Updated on every ingest. LLM reads first to find relevant pages.
- **log.md** — chronological. Append-only. Parseable with grep. Timeline of wiki evolution.

## Why It Works
Tedious part of knowledge base = bookkeeping (cross-references, consistency, staleness). Humans abandon wikis because maintenance burden grows. LLMs don't get bored, don't forget cross-references, can touch 15 files in one pass.

Human's job: curate sources, direct analysis, ask questions, think.
LLM's job: everything else.

## Application to Our Framework
- llm-wiki/ is our persistent knowledge layer
- index.md lets agents find relevant knowledge without re-deriving
- log.md tracks what's been done across sessions
- Knowledge compounds: research → wiki entries → informs architecture → informs implementation
- Schema = AGENTS.md + skills/ definitions

## Source
- _sources/llm-wiki.md (original pattern document)
- Related: Vannevar Bush's Memex (1945) — private curated knowledge with associative trails
