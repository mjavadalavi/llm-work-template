# RTK (Rust Token Killer)

## What
High-performance CLI proxy that minimizes LLM token consumption by filtering CLI command output. 60-90% token savings.

## Architecture
Command proxy: `main.rs` routes CLI commands via Clap enum to specialized filter modules in `src/cmds/*/`. Each module executes underlying command + compresses output. Token savings tracked in SQLite.

## Key Design Principles

### Correctness vs Token Savings
- Default output → aggressive compression
- Verbose flags (user explicitly asked) → pass-through more
- When in doubt → preserve correctness

### Transparency
- Filtered output must look like original command's output
- No new formats, headers, or markers
- Indistinguishable from "shorter version of real command"

### Never Block
- If filter fails → fall back to raw output
- RTK never prevents command execution
- Every filter needs fallback path

### Zero Overhead
- <10ms startup
- No async runtime
- No config I/O on critical path
- `lazy_static!` for all regex

## Supported Ecosystems
git/gh/gt, cargo, go/golangci-lint, npm/pnpm/npx, ruff/pytest/pip/mypy, rspec/rubocop/rake, dotnet, playwright/vitest/jest, docker/kubectl/aws

## Filter Types
| Use TOML filter when | Use Rust module when |
|---|---|
| Plain text, predictable lines | Structured output (JSON, NDJSON) |
| Regex filtering achieves 60%+ | Needs state machine parsing |
| No flag injection needed | Needs to inject flags like `--format json` |
| No cross-command routing | Routes to other commands |

## Token Tracking
- SQLite database tracks per-command savings
- `rtk gain` shows aggregate stats
- `rtk gain --history` shows per-command breakdown
- Proxy mode: `rtk proxy <cmd>` for unfiltered but tracked execution

## Relevance to Our Framework
- Can be used by agents to reduce token consumption on bash commands
- Especially useful for: test output, lint output, git operations
- Integrates via shell hooks (transparent command rewriting)
- Agent doesn't need to know RTK is involved

## Source
- rtk-ai/rtk (CLAUDE.md, CONTRIBUTING.md, CHANGELOG.md)
