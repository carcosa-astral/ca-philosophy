# CLAUDE.md: Standards for All Projects

This file applies to every project. Project-specific notes go in that project's own README.md. Projects do not get their own CLAUDE.md. If the README and this file ever disagree, ask Griff.

## About the owner

- Griff is not a full-time programmer. Claude handles most of the code.
- Explain what you are doing in short, clear steps. Griff has ADHD, so no walls of text.
- When you need a decision, ask a multiple-choice question with purposeful options.
- For big tasks, show a short plan in plain steps first, then start building. Do not wait for approval unless a decision is needed.
- Never edit this file. If a rule here seems wrong or outdated, tell Griff and ask. Griff makes the change.
- If an error cannot be fixed after a few tries, stop. Explain in plain words what failed, then offer two or three ways forward as a multiple-choice question.
- Do not use em dashes in any writing, code comments, or docs.
- When recommending a tool, include a short setup walkthrough.

## Philosophy

- Software should be snappy, good looking, and contain nothing the user does not use.
- We borrow nothing. We build from our own code and our own specs, every time.
- No bloat, no background services, no telemetry, no features nobody asked for.
- Every line of code and every byte shipped must earn its place.
- If a choice is between "faster to build" and "lighter to run", lighter wins unless Griff says otherwise.
- Small focused files: one job per file. Split any file that grows past a few hundred lines.
- Before every commit: add tests for logic that is easy to get wrong, and run the app once to confirm it works. No need for tests on everything.
- All projects are for Griff's personal use. They are not built for production at scale, for multiple customers, or for sale. Do not add multi-user, multi-tenant, or scaling features unless Griff asks.

## Desktop applications

### Language

- Rust (stable toolchain, 2021 edition or newer).
- Not .NET, not Electron, not any web view (no WebView2, no Tauri).
- Output must be a single native executable with no prerequisite runtime for the user to install.

### Platforms

- Windows first. Build and test on Windows before anything else.
- Code must stay cross-platform capable (macOS, Linux). Do not use Windows-only APIs unless they are isolated behind a small platform module with a clear interface, so other platforms can be added later.
- Cross-platform is a design rule, not a promise for every release. Windows ships first.

### Delivery and data

- Deliver a portable single `.exe` that runs from any folder. No installer unless Griff asks.
- Store settings and data next to the `.exe`, in plain, readable files. Nothing hidden in system folders, no registry entries.

### Performance

- Fast startup, low memory, small binary.
- Release builds use `opt-level = 3`, `lto = true`, `codegen-units = 1`, `strip = true`, `panic = "abort"` unless a project has a reason not to.

### Dependencies (strict)

- Zero external crates. Standard library plus our own code. Build it ourselves, to spec.
- Calling the operating system directly is not borrowing. Write our own minimal bindings to OS APIs (for example Win32 on Windows) instead of pulling in a binding crate.
- Never add a crate on your own. Only Griff can approve one, and only when he says so specifically.
- If Griff approves one, record it in the project's README under "Approved dependencies" with the date and reason.
- If an approved crate is only a stopgap, mark it "temporary" and note what will replace it.

### UI

- No web views and no heavy third-party UI frameworks by default.
- Long-term goal: our own in-house UI library, built from our own design spec (colors, spacing, type scale, widgets), reused across all apps. It lives in its own repo.
- Build the UI library in small steps. Each app should only pull in the widgets it needs.
- Platform plumbing (opening a window, reading input, drawing pixels, rendering text) is the hardest part to write from scratch. We still write it ourselves. Build it in small, testable pieces, one platform at a time, and keep each platform's code behind a shared interface.
- If a piece looks unreasonably hard (for example full font shaping or accessibility), stop and tell Griff the options before choosing. Do not borrow quietly.
- Keep UI code separate from app logic, so logic can be tested without a window.

### Code quality

- `cargo fmt` and `cargo clippy` must pass with no warnings before any commit.
- Prefer clear, boring code over clever code. Griff must be able to follow what it does.
- Comments explain why, not what.
- Handle errors explicitly. No `unwrap()` or `expect()` in app code unless a crash is the correct behavior, and say why in a comment.

## Web apps and websites

### Hosting: always Cloudflare

- Everything that lives on the web runs on Cloudflare. All of Griff's domains are already in Cloudflare.
- Never ask where to host or how to run something. The answer is always Cloudflare.
- Never use or suggest other hosts or platforms (Vercel, Netlify, Render, Deno Deploy, and similar), private servers, or VPS.
- No Docker for now. Griff has no good setup for it. Do not suggest it.
- Keep it free wherever possible. Griff already pays $5 per month for Cloudflare image and video features, so use those for images and video. Before using anything that costs extra, tell Griff the cost and wait for a yes.

### Stack

- Cloudflare Workers for all server-side code. Serve the front end from the same Worker using Workers static assets (not Pages).
- D1 for databases.
- R2 for file storage (the S3 equivalent), and Cloudflare Images and Stream for images and video.
- Turnstile for bot protection on any public form.
- Our own personal CDN: serve all assets from Griff's own domains through Cloudflare. No third-party CDNs, no external script tags, no hosted fonts.
- Other Cloudflare services (KV, Queues, Durable Objects, Access, and so on) are fine when they are the simplest fit. Pick without asking, as long as they stay free.
- Put Cloudflare Access (the free login wall) in front of every app that only Griff uses. Public websites do not get it. Do not write custom login code.
- Do not build for scale. One user, simple data, simple code.

### Language and dependencies

- Workers code is TypeScript.
- Front end is plain HTML, CSS, and JavaScript modules. No frameworks (React, Next, Vue, and similar) and no UI libraries.
- Wrangler is the only pre-approved dependency, as a dev tool. Everything else follows the same rule as desktop: never add a package on your own, only Griff can approve one.
- Record approved packages in the project's README under "Approved dependencies" with the date and reason.

### Wrangler and deploys

- Wrangler does everything: create resources, run local dev, run D1 migrations, set secrets, and deploy.
- Config lives in `wrangler.jsonc`. Non-secret settings go there. Secrets never do.
- Create resources with Wrangler commands (`wrangler d1 create`, `wrangler r2 bucket create`, and so on), not by clicking around in the dashboard.
- Run `wrangler deploy` after every push, from Griff's machine. Order is commit, push, then deploy. Deploys are not triggered by GitHub.
- If a deploy fails, tell Griff in plain words what failed and what you will try next.
- Remote D1 migrations that drop or rewrite existing data need Griff's yes first, because deploys run automatically.
- Attach each project to a custom domain on one of Griff's Cloudflare domains through the Wrangler config.

### Secrets and environment

- All API keys and secrets live in a local `.env` file in the project root. This is the single source of truth.
- Push secrets from `.env` to Cloudflare with Wrangler (`wrangler secret bulk`). Confirm the exact syntax with `wrangler secret bulk --help` the first time in a project.
- Keep a `.env.example` with the variable names only and no values, so the list of needed secrets is documented.
- `.env` must never be committed to git and must be in `.gitignore` before the first commit.
- Never print, log, or paste secret values in chat, code, or docs.

## Design and look (UI/UX)

Applies to desktop apps and web apps.

- Never assume which design to use. At the start of UI work on each project, ask Griff with a multiple-choice question:
  - Use the Hali design system.
  - Use a design spec Griff provides for this project.
  - Something else, described by Griff.
- Hali is an option, not the default. Griff may skip it.
- Once chosen, record the decision in the project's README under "Design" and follow that spec exactly. Do not mix in styles from other sources.
- Ask again for each new project, even if the last one used Hali.
- Dates and times: store in UTC, display in US Eastern with a 12-hour clock.
- Accessibility baseline for every UI: everything works with the keyboard alone, and text has readable contrast. Where the chosen design spec conflicts with this, tell Griff before building.

## Windows scripting

- Tiny, single-purpose scripts are Batch or PowerShell. Anything bigger becomes a Rust `.exe` that follows the desktop rules above (including no external crates).
- Helper scripts (.bat, .ps1) go in `C:\tools`, which is on PATH.
- Griff's RMM terminal starts in Command Prompt. Write command lines that run from cmd without switching shells, using `powershell -NoProfile -Command "..."` or an encoded command when PowerShell is needed.

## New project checklist

Do these in order. Do not skip ahead.

1. Prompt Griff to create a new private GitHub repo, and wait until he has done it. Repos are private by default.
2. Ask Griff to import the design first: the artifacts or the design PDF showing how it should look. Save them in a `design/` folder in the repo. Do not build anything visual until Griff has provided the design or said there is none.
3. Ask Griff which license to use. Never pick one by default, even if earlier projects used a certain one.
4. Set the git identity (see Git and versioning).
5. Create README.md (see README below), CHANGELOG.md (with an Unreleased section), LICENSE, and `.gitignore`.
6. Web projects: also create `.env` and `.env.example`, with `.env` listed in `.gitignore`, before the first commit.
7. Start at version 0.1.0 unless Griff says otherwise.
8. Make the first commit on `main` and push it.

## Git and versioning

### README

- Every README is full documentation. It covers:
  - What the project is and its current version.
  - Features.
  - How to install, run, and build it.
  - A usage guide.
  - Architecture notes: how the code is organized and why.
  - Approved dependencies, with date and reason.
  - Design: which design spec was chosen.
  - Configuration: the names of any environment variables (never values).
  - License and a link to CHANGELOG.md.
- Keep the README current. Update it in the same commit as the change that makes it out of date.

### Branches

- Only `main`. No other branches, no pull requests, no forks.
- Never force push or rewrite history without asking Griff first.
- If a problem is found in history that is already pushed (for example a commit with the wrong email), fix it with a new commit. Never rewrite pushed history.

### Identity

- Griff's GitHub account is `carcosa-astral`.
- Before the first commit in any repo, set the identity explicitly:
  - `git config user.name "Carcosa Astral"`
  - `git config user.email "337445296+carcosa-astral@users.noreply.github.com"`
- Never use any other name or email, including the defaults on this machine or on any account.
- Before every push, run `git log -n 5 --format='%an <%ae>'` and confirm every new commit uses the name and email above. If not, fix it before pushing.

### Commits

- Commit after each working change. Every commit must leave the project in a working state.
- Use Conventional Commits: `type(scope): description`.
  - Types: `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `chore`.
  - Lowercase, imperative, no period, about 72 characters or less. Scope is optional.
  - A breaking change adds `!` after the type or scope, like `feat!: change save format`.
- Push to GitHub after every commit.
- Never commit secrets. `.env` stays out of git.
- Update the Unreleased section of CHANGELOG.md as part of the same change, not later.

### Versioning

- Semantic versioning: MAJOR.MINOR.PATCH. New projects start at 0.1.0.
- MAJOR is a breaking change, MINOR is a new feature, PATCH is a fix. Before 1.0.0, a breaking change bumps MINOR. Move to 1.0.0 only when Griff says so.
- Always keep versioning. Every project has a version, a changelog, and tags from the first commit onward.
- CHANGELOG.md follows Keep a Changelog format: Added, Changed, Deprecated, Removed, Fixed, Security.

### Releases

- Release automatically after each finished feature, or after a standalone fix.
- Tell Griff which bump was chosen and why, in one sentence.
- Release steps:
  1. Move the Unreleased entries under the new version heading with today's date.
  2. Update the version number wherever the project stores it (for example `Cargo.toml` or `package.json`).
  3. Commit with `chore(release): vX.Y.Z`.
  4. Create an annotated tag `vX.Y.Z` on that commit (for example `v1.2.0`).
  5. Push the commit and the tag.
- Never move, delete, or reuse a tag without asking Griff first.
