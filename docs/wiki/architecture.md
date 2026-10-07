# architecture

Settled design decisions and their rationale. Update this file (plus
`index.md` and `log.md`) in the same commit as any decision. Research context
lives in `research/`; living state lives in `progress.md`.

## Decisions

| Decision | Status | Rationale |
| --- | --- | --- |
| Workspace with `app-core` (pure) + `app-cli` (I/O) | adopted | Failures localize; core testable without fs/network |
| Strict `[workspace.lints]`, opt-in per crate | adopted | Compiler as verification; see root `Cargo.toml` |
| Suppressions via `#[expect(..., reason)]` only | adopted | Stale suppressions become compile errors |
| llm-wiki (`docs/raw/` + `docs/wiki/`) under `docs/` | adopted | One root entry per system; `docs/raw/` immutable sources, `docs/wiki/` generated knowledge (supersedes root-level `raw/` + `wiki/` layout) |
| CI `docs-gate`: behavior PRs need docs or exemption | adopted | Honor-system checkboxes do not survive agents; gate keys off the PR template's exemption box |
| Conventional-commit subjects (lefthook hook + CI job) | adopted | Local hook for speed, CI job for `--no-verify`/web edits; same regex both places |
| `CHANGELOG.md`, version bumped at release time | adopted | Per-PR bumps are noise; docs-gate covers changelog updates on behavior changes |
| CI `template-check`: leftover placeholders fail | adopted | Setup drift is silent (a derived repo shipped with the template README); name-bypassed on the template itself so forks and template PRs pass |
| Simplicity rules: YAGNI/KISS, rule of three, smallest diff | adopted | Abstractions are misunderstanding surface for LLM-written code; countable rules beat adjectives |
| Floating stable toolchain + CI-verified MSRV floor | adopted | Stable drift caught a real lint; pinning would hide that signal. MSRV declared in `Cargo.toml`, verified by CI `msrv` job |

## Open questions

- _None yet. Move settled rows to the table above with rationale._
