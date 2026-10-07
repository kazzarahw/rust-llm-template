## What changed

<!-- One-line summary. -->

## Wiki updates (required if behavior, decisions, or state changed)

<!-- CI `docs-gate` enforces this section: a PR touching `crates/` must change
  `docs/`, `README.md`, `CHANGELOG.md`, or `AGENTS.md`, or tick the exemption. -->

- [ ] `docs/wiki/` updated: new/changed pages listed in `docs/wiki/index.md`
- [ ] `docs/wiki/log.md` appended with `## [YYYY-MM-DD] <op> | <title>` entry
- [ ] New source material (if any) added under `docs/raw/` as `YYYY-MM-DD-slug.md`, unmodified thereafter
- [ ] No wiki change needed (pure refactor with no behavior/decision impact)

## Verification

<!-- Paste actual results. Never report success while any fail. -->

- [ ] `cargo fmt-check`
- [ ] `cargo lint`
- [ ] `cargo t`
- [ ] `cargo test --doc --workspace`
- [ ] `cargo doc-check`
- [ ] `cargo deny check`
- [ ] `typos`
