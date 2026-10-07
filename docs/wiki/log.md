# log

Append-only chronological record of wiki events. Never rewrite history.
Format: `## [YYYY-MM-DD] <op> | <title>`, where `<op>` is `ingest`, `query`,
`lint`, `decision`, or `progress`.

Tip: `grep "^## \[" docs/wiki/log.md | tail -5` shows the last 5 events.

## [2026-10-06] progress | Template scaffolded

- Created with hardened workspace: lints, toolchain, aliases, CI, deny,
  lefthook, editorconfig, typos.
- Replaced `docs/` with llm-wiki: `raw/` + `wiki/` + schema in `AGENTS.md`.
- Next: rename crates, set OWNER/REPO, rewrite overview/progress for the real
  project, ingest first source.

## [2026-10-06] decision | Fixed ci-success workflow (shell var in expression)

- First CI run on `main` died before any job started ("workflow file issue").
- Root cause: `ci-success` used `${{ needs.$job.result }}` inside a shell loop.
  `needs.<job>` requires a literal job ID; a shell variable is a workflow
  parse error. Rewrote with one explicit `needs.<id>.result` check per job.
- The faulty pattern had been copied verbatim into this template; fixed here.
- `wiki/index.md` intentionally untouched: no pages added or removed.

## [2026-10-06] decision | Solo-friendly ruleset (0 required approvals)

- The initial `main` ruleset required 1 approving + code-owner
  review. Solo maintainer authoring the PR can never satisfy that: GitHub does
  not count the author's own approval, so every PR deadlocks. Same latent issue
  would hit any solo-maintainer repo applying that ruleset.
- Relaxed to `required_approving_review_count: 0`, code-owner/last-push
  approval off. Still enforced: PRs, linear history, `ci-success`, no force
  pushes, no deletion. `.github/rulesets/main.json` updated to match.

## [2026-10-07] progress | Template housekeeping pass

- Removed predecessor-repo references from `README.md`, `wiki/progress.md`,
  `wiki/log.md` (one-time history rewrite with owner approval; the referent no
  longer exists). `wiki/index.md` untouched: no pages added or removed.
- Hid toolchain configs as dotfiles: `.clippy.toml`, `.rustfmt.toml`,
  `.lefthook.yml`, `.cargo/deny.toml`; folded typos into
  `Cargo.toml [workspace.metadata.typos]`; dropped redundant clippy `msrv`
  line (read from `rust-version`).
- Unified setup markers to `TODO(template)`; trimmed `.gitignore` JetBrains
  noise; added `raw/assets/.gitkeep`.

## [2026-10-07] progress | Knowledge system consolidated under docs/

- Moved `raw/` → `docs/raw/`, `wiki/` → `docs/wiki/` (one root entry per
  system; `../raw/` relative links survive unchanged). Historical log entries
  above keep their original paths.
- Updated references in `AGENTS.md`, `README.md`, `.github/CODEOWNERS`,
  `.github/PULL_REQUEST_TEMPLATE.md`, `docs/` READMEs; superseded the
  root-level layout row in `docs/wiki/architecture.md`.

## [2026-10-07] progress | Enforcement pass: docs-gate, commit lint, changelog

- CI `docs-gate`: PRs touching `crates/` must change `docs/`, `README.md`,
  `CHANGELOG.md`, or `AGENTS.md`, or tick the PR template exemption.
  Pushes to main pass trivially (gated on the PR side).
- CI `commits` + lefthook `commit-msg` enforce Conventional Commits subjects
  (same regex both places); `ci-success` covers both new jobs.
- Added `CHANGELOG.md` (release-time versioning) and a README release
  checklist; documented red-CI and small-commit principles in `AGENTS.md`.
- `docs/wiki/index.md` untouched: no pages added or removed.

## [2026-10-07] progress | Template setup self-check

- CI `template-check`: fails derived repos carrying placeholders (owner,
  crate names, `TODO(template)`, copyright, placeholder source, unrenamed
  crate dirs). Bypassed by repository name on the template itself, so the
  template and contributor forks pass; wired into `ci-success`.
- `docs/wiki/index.md` untouched: no pages added or removed.

## [2026-10-07] progress | Paradigm guidance refresh

- Named KISS/YAGNI/DRY with countable rules (rule of three, smallest diff,
  delete dead code); clarified no-new-macros and xtask scope; corrected
  pedantic warn-vs-deny wording.
- Documented floating-stable + CI-verified-MSRV setup; added CI `msrv` job
  (`cargo +1.93 check`, verified locally with a real 1.93 toolchain).
- `docs/wiki/index.md` untouched: no pages added or removed.
