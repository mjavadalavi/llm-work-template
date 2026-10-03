# Caveman Encoding

## What
Token-compressed language for LLM-facing documents. ~75% fewer tokens than prose while staying precise.

## Grammar Rules
1. Drop articles (a, an, the)
2. Drop filler (just, really, basically, simply, actually)
3. Drop aux verbs where fragment works
4. Drop hedging, pleasantries
5. Fragments fine
6. Short synonyms: fix > implement, run > execute, big > extensive

## Symbol Set

| Symbol | Meaning |
|--------|---------|
| → | leads to / becomes / triggers |
| ∴ | therefore / fix |
| ∀ | for all / every |
| ∃ | exists / some |
| ! | must / required |
| ? | may / optional |
| ⊥ | never / forbidden / nil |
| ≠ | not equal |
| ∈ | in / member of |
| ∉ | not in |
| ≤ | at most |
| ≥ | at least |
| & | and |
| \| | or |
| § | section reference |

## Preserve Verbatim
Never compress: code blocks, paths, URLs, identifiers, numbers, error strings, SQL, regex, JSON, YAML, quoted strings.

## Examples
- "The system must ensure all requests are authenticated" → "∀ req → auth ! before handler"
- "This task depends on auth middleware" → "T3 cites V1 & I.auth"
- "Bug: token comparison used < instead of ≤" → "B1|2026-04-20|token `<` ≠ `≤`|V2"

## Boundaries
- User asks prose explanation → switch to normal English
- External review docs → normal English
- Commit messages → normal English
- Code comments → normal English

## Why It Works
Spec loaded every invocation. 75% fewer tokens = 75% fewer dollars & faster reads. Symbols unambiguous. Human skims fast too.

## Source
- Cavekit FORMAT.md + caveman skill (JuliusBrussee/cavekit)
- Related: [caveman](https://github.com/JuliusBrussee/caveman) (standalone compression skill)
