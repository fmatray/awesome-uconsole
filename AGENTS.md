# Repository Guidelines

Guidance for AI assistants working in this repository.

## Project Overview

`awesome-uconsole` is a curated "awesome" list for the ClockworkPi uConsole — a handheld Linux terminal with a 6-inch screen and integrated keyboard (CM4, R01, or A06 cores). Content lives entirely in `README.md`. Licensed under GPL-3.0 (`LICENSE`).

**State: active content repo.** No source code, no build system, no dependencies. All work is Markdown curation: finding, verifying, and organizing links.

## Architecture & Data Flow

The entire tracked tree:

- `README.md` — the awesome list (the only content file)
- `LICENSE` — GPL-3.0 full text
- `AGENTS.md` — this file
- `.gitignore` — excludes `local_cache/` (tooling residue) and `todo`

No modules, no data flow, no code paths. `local_cache/` is **untracked** tooling residue from the codebase-memory indexer; never commit or read it as project content.

## Key Directories

- `/` (repo root) — the whole project; flat structure, no subdirectories.
- `local_cache/` — ~127 MB embedding-model cache. Ignored via `.gitignore`. Do not commit.

## Development Commands

No package manifest, Makefile, or task runner. The only commands:

```sh
git add README.md && git commit -m "..." && git push origin main
curl -s -o /dev/null -w "%{http_code}" -L -A "Mozilla/5.0 ..." <url>   # link checks
```

## Content Workflow

Every link addition or edit follows this workflow:

1. **Find candidates** — web search, or GitHub API (`api.github.com/search/repositories?q=uconsole&sort=stars`) for community projects sorted by stars.
2. **Verify before adding** — never add an unverified URL:
   - `curl -s -o /dev/null -w "%{http_code}" -L -A "Mozilla/5.0 ..." <url>` — expect 200.
   - GitHub repos: check via `api.github.com/repos/<owner>/<repo>` or confirm in the org listing.
   - Printables: 403s curl; verify via GraphQL API `api.printables.com/graphql` with `query { print(id: "ID") { name } }`.
   - Reddit/eBay/Amazon: bot-block curl (403/503). Accept search-engine-indexed pages as evidence.
   - Soft-404s: inspect page content (`og:title`, `<title>`) — a generic site title means the page does not exist.
3. **Add in README structure** — `- [Name](url) — short description` under the right category.
4. **Commit and push** — one topic per commit, imperative subject line.

When removing broken links: replace with the real verified resource if one exists (e.g., a fabricated repo name → the actual repo in the `clockworkpi` org), otherwise delete the line.

## Content Rules

- Write only in English.
- Keep descriptions short — one clause, lowercase start, no trailing period.
- Bullet format exactly: `- [Name](url) — description`.
- Never fabricate URLs, repo names, or product pages. Every URL must have been verified live (or API-confirmed) before it enters the list.
- **Ordering**: within each section or subsection, entries MUST be sorted alphabetically by name (case-insensitive).
- **Hardware platform split**: each Hardware subsection (`### 3D print and Cases`, `### Electronics`, `### Accessories`) MUST be split into three platform groups in this order:
  1. `#### CM4 / CM5` — entries for Raspberry Pi CM4 and CM5 cores
  2. `#### Radxa CM5` — entries specific to Radxa CM5
  3. `#### Others (CM3, A06, etc.)` — entries for CM3, CM4S, A06, or platform-agnostic
  Use `*(none yet)*` placeholder if a group is empty.
- **Resellers split**: the `## Resellers` section MUST be divided into:
  - `### uConsole resellers (official / authorized)` — shops officially affiliated with ClockworkPi
  - `### Third-party / marketplace` — unofficial channels, marketplaces, third-party hardware vendors
  A reseller can appear in both categories if applicable. Each entry MUST include country in parentheses at the end of the description, e.g., `(China)`, `(Austria)`, `(Czech Republic)`. Multiple countries allowed: `(China / global)`.
- Categories (keep this structure):
  - `## Official` — clockworkpi.com pages, wiki, forum, GitHub org
  - `## Community` — Telegram, Discord, Reddit
  - `## Resellers` — shops selling uConsole; flag unofficial channels (e.g., "no official support")
  - `## OS and kernel` — official images, kernels, community OS builds
  - `## Hardware` — with subsections: `### 3D print and Cases`, `### Electronics`, `### Accessories`
  - `## Software` — drivers, apps, games for the uConsole
  - `## Related devices` — DevTerm, PicoCalc, GameShell
- Update the `*Last updated: YYYY-MM-DD*` footer line on content changes.

## Important Files

- `README.md` — the project's only content and entry point.
- `LICENSE` — GPL-3.0 v3, 2007 FSF text. All contributions fall under it. (No copyright holder line filled in yet.)
- `.gitignore` — keeps `local_cache/` and `todo` out of the repo.

## Runtime/Tooling Preferences

No runtime, package manager, or toolchain is mandated. `curl` (with a browser User-Agent) and `jq` suffice for link verification. Do not introduce a link-checker dependency; re-verify manually per the workflow above. If a CI link-checker is ever added, record it here.

## Testing & QA

No tests, CI, linters, or QA tooling; `.github/` does not exist. The quality gate is the verification step of the content workflow: every URL in `README.md` must return HTTP 200 (or be API-confirmed) — spot-check old links when touching a section, and re-check any link reported broken.