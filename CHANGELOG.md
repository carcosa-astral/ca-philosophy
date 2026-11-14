# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- New project checklist step 1: refresh `CLAUDE.md` from this repo before starting. Claude Code clones or pulls the repo, copies the file to the `.claude` folder, reports any version change, and stops to ask if the repo cannot be reached.

## [1.1.1] - 2026-11-14

### Added

- Version line in the header of `CLAUDE.md`.

### Removed

- Tag and release links from this changelog. This repo does not use git tags or GitHub releases. The version lives in the `CLAUDE.md` header.

## [1.1.0] - 2026-11-14

### Changed

- Every project now uses the MIT License. Claude Code no longer asks which license to use.

## [1.0.0] - 2026-11-14

### Added

- `CLAUDE.md` with the global coding standards: philosophy, desktop applications (Rust), web apps (Cloudflare), design and look, Windows scripting, new project checklist, and git and versioning.
- `README.md` with full documentation.
