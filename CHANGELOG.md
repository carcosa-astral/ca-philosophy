# Changelog

All notable changes to this project are documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.8.0] - 2026-11-15

### Changed

- Scripts: each script now lives in its own folder under `C:\tools` (also its git repo) with a `data` subfolder, and gets a one-line `.cmd` launcher in `C:\tools`. This replaces the bare `.py` in `C:\tools` and the `PATHEXT` approach.
- Python packages are also recorded in the README, with the `pip install` command.

## [1.7.0] - 2026-11-15

### Changed

- "Windows scripting" is now "Scripts", moved next to Desktop applications and Web apps.

### Added

- Python packages: same rule as crates. Borrow a pip package only for big jobs or security.

## [1.6.0] - 2026-11-15

### Added

- "Security basics" section: private by default, keys not passwords, firewall closed by default, automatic updates, one user per service, backups, static public pages.

## [1.5.2] - 2026-11-15

### Changed

- Dependencies: borrow a crate mostly when the job is big or when building it ourselves could weaken security. Everything else is built in house.

## [1.5.1] - 2026-11-15

### Added

- New rule in "About the owner": explain everything in plain words with simple everyday comparisons.

## [1.5.0] - 2026-11-15

### Changed

- Outside Rust crates are now allowed. The "Dependencies (strict)" rules became "Dependencies": keep the count small, prefer well-known crates, record each one in the README.
- "We borrow nothing" now reads "own code and specs first".
- Windows scripting: scripts on Griff's PC are Python, run by bare name from `C:\tools` through `PATHEXT`, with a `.bat` shim as the fallback. Batch and PowerShell scripts are no longer the default.

## [1.4.0] - 2026-11-14

### Added

- `NEW-PROJECT.md` now accepts an optional spec document. If one is attached, it overrides the day one features list and Claude Code skips feature questions.

### Changed

- `NEW-PROJECT.md` now includes the raw URL for `CLAUDE.md` in the message itself, so Claude Code knows exactly where to download the standards.

## [1.3.0] - 2026-11-14

### Added

- `NEW-PROJECT.md`: a starter message to paste into Claude Code for every new project. It expects a design PDF attached, summarizes the design for confirmation before building, and asks its starting questions in one round.

## [1.2.1] - 2026-11-14

### Fixed

- New project checklist step 1 now downloads `CLAUDE.md` directly from the raw URL on the `main` branch of this repo and saves it unchanged in the new project. No clone, and nothing in the user profile folder.
- Every project now holds an unmodified copy of `CLAUDE.md`. Updated the header, the "never edit" rule, and the README to match.

## [1.2.0] - 2026-11-14

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
