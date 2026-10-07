# rust-llm-template

<!-- TODO(template): replace the title, description, status, and setup checklist
  below for your project. `grep -r "TODO(template)"` lists all setup tasks. -->

A GitHub template repo for strictly verified Rust programs written with an LLM.
Hardened workspace (strict lints, toolchain, CI, hooks) with project knowledge
in a Karpathy-style llm-wiki under `docs/` (`docs/raw/` + `docs/wiki/`).

Click **Use this template** to create a new repo. Then work through the
setup checklist below.

## Status

Fresh template. Scaffold builds; no application logic yet.

## Layout

- `crates/app-core` — pure logic; no I/O
- `crates/app-cli` — the `app` binary; all I/O lives here
- `docs/raw/` — immutable source material for the wiki
- `docs/wiki/` — LLM-maintained knowledge base (`index.md`, `log.md`,
  `overview.md`, `architecture.md`, `progress.md`, `research/`, `queries/`)
- `AGENTS.md` — project conventions + wiki schema (source of truth)
- Toolchain configs (all dotfiles at root, except where the tool fixes the
  path): `.cargo/config.toml` (aliases) + `.cargo/deny.toml` (dependency
  policy), `.clippy.toml`, `.rustfmt.toml`, `.lefthook.yml`,
  `rust-toolchain.toml`; `typos` config lives in root `Cargo.toml`
  (`[workspace.metadata.typos]`)

## Setup checklist (do this once per new repo)

- [ ] Replace `kazzarahw/rust-llm-template` in root `Cargo.toml` (`repository`).
- [ ] Rename `app-core` / `app-cli` / `app` to your names. Update:
  `.cargo/deny.toml` `skip-tree`, `README.md`, `AGENTS.md`, crate `Cargo.toml` files.
- [ ] Replace `@kazzarahw` in `.github/CODEOWNERS` with your username or team.
- [ ] Set copyright holder in `LICENSE`.
- [ ] On GitHub: Settings > General > check **Template repository** (for the
  template itself). For each new repo: apply the ruleset below, enable
  Dependabot, install hooks (`lefthook install`).
- [ ] Install tooling: `cargo-nextest`, `cargo-deny`, `cargo-mutants`, `typos`,
  `lefthook`.
- [ ] Rewrite `docs/wiki/overview.md`, `docs/wiki/progress.md`,
  `docs/wiki/index.md`, `docs/wiki/log.md` for your project. Ingest your first
  source into `docs/raw/`.

Apply the repo ruleset (maintainer only):

```sh
gh api --method PUT repos/kazzarahw/rust-llm-template/rulesets \
  --input .github/rulesets/main.json
```

## Development

Requires a stable Rust toolchain (edition 2024, MSRV 1.93). The pinned
components live in `rust-toolchain.toml`, so `rustup` will fetch them
automatically.

```sh
cargo build
cargo fmt-check
cargo lint
cargo t
cargo test --doc --workspace
cargo run
```

Aliases live in `.cargo/config.toml`. See `AGENTS.md` for the full list, the
wiki workflows (ingest / query / lint), and the verification rules this repo
enforces.

## Wiki quickstart

```sh
# Ingest: drop a source, then ask the agent to ingest it.
# The agent updates docs/wiki pages, docs/wiki/index.md, and appends to docs/wiki/log.md.
cp article.md docs/raw/2026-10-06-article-slug.md
```

Log format: `## [YYYY-MM-DD] <op> | <title>` where `<op>` is
`ingest`, `query`, `lint`, `decision`, or `progress`.

## License

MIT. See [LICENSE](LICENSE).
