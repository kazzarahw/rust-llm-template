# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Fixed

- Test assertion uses `assert_ne!` for compatibility with the stable
  `clippy::assert_is_empty` lint.

### Changed

- Knowledge system consolidated under `docs/` (`docs/raw/` + `docs/wiki/`).
- Toolchain configs hidden as dotfiles; typos config embedded in `Cargo.toml`.
- CI enforces docs updates for behavior changes (`docs-gate`) and
  Conventional Commits subjects (lefthook hook + `commits` job).

## [0.1.0] - 2026-10-06

### Added

- Initial template scaffold: hardened workspace, llm-wiki skeleton, CI,
  hooks, and verification gates.
