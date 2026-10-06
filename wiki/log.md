# log

Append-only chronological record of wiki events. Never rewrite history.
Format: `## [YYYY-MM-DD] <op> | <title>`, where `<op>` is `ingest`, `query`,
`lint`, `decision`, or `progress`.

Tip: `grep "^## \[" wiki/log.md | tail -5` shows the last 5 events.

## [2026-10-06] progress | Template scaffolded

- Created from `iji` hardening: workspace lints, toolchain, aliases, CI, deny,
  lefthook, editorconfig, typos.
- Replaced `docs/` with llm-wiki: `raw/` + `wiki/` + schema in `AGENTS.md`.
- Next: rename crates, set OWNER/REPO, rewrite overview/progress for the real
  project, ingest first source.
