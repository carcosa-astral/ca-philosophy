# ca-philosophy

The global coding standards and working philosophy for all of Griff's projects. One file, `CLAUDE.md`, that Claude Code reads at the start of every session so every project stays consistent.

Current version: **1.1.1**

## What it is

A plain markdown instruction file. It tells Claude Code how Griff wants software built, versioned, and delivered: what language to use, what to never borrow, where things run, how the work is committed, and how to communicate.

## What it covers

- **About the owner:** how to communicate, how to ask questions, how to handle big tasks and stuck work.
- **Philosophy:** snappy, no bloat, borrow nothing, personal use only, small focused files, light testing.
- **Desktop applications:** Rust, Windows first and cross-platform capable, no web views, zero external crates, portable single `.exe`, data stored next to the `.exe`.
- **Web apps and websites:** always Cloudflare (Workers, D1, R2, Images and Stream, Turnstile, Access), TypeScript, plain HTML, CSS and JavaScript, Wrangler for everything, secrets from a local `.env`.
- **Design and look:** ask which design to use for each project (Hali is an option, never the default), accessibility baseline, date and time display.
- **Windows scripting:** tiny scripts in Batch or PowerShell, anything bigger in Rust.
- **New project checklist:** the order of steps for every new project.
- **Git and versioning:** `main` only, Conventional Commits, push after every commit, semantic versioning, Keep a Changelog, annotated tags.

## How to install

1. Copy `CLAUDE.md` to `C:\Users\<you>\.claude\CLAUDE.md`.
2. Start a new Claude Code session. It loads the file automatically in every project.

To update, replace that file with the newest `CLAUDE.md` from this repo.

## Usage

- This repo is the source of truth. Edit `CLAUDE.md` here, then copy it to the `.claude` folder.
- Claude Code never edits this file. If it thinks a rule is wrong or outdated, it tells Griff and asks.
- Projects do not get their own `CLAUDE.md`. Project-specific notes go in each project's README.

## Architecture

The repo is intentionally tiny:

- `CLAUDE.md`: the standards themselves.
- `README.md`: this file.
- `CHANGELOG.md`: version history.
- `LICENSE`: MIT.

Each meaningful change to the rules gets a version bump and a changelog entry. The current version is stored in the header of `CLAUDE.md`. This repo does not use git tags or GitHub releases.

## Approved dependencies

None.

## Design

Not applicable. This repo has no UI.

## Configuration

None. No environment variables or secrets.

## License

MIT. See [LICENSE](LICENSE).

## Changelog

See [CHANGELOG.md](CHANGELOG.md).
