# Repository Guidelines

Guidance for AI assistants working in this repository.

## Project Overview

`awesome-uconsole` is a brand-new repository (single initial commit) that appears intended as a curated "awesome" list for the [ClockworkPi uConsole](https://clockworkpi.com/product/uconsole) — a handheld Linux terminal/AI device. The `README.md` currently contains only the title; all content is yet to be added. Licensed under GPL-3.0 (`LICENSE`).

**State: scaffold.** There is no source code, no build system, no tests, and no dependencies. Do not assume any tooling exists — verify before running any command beyond `git`.

## Architecture & Data Flow

No architecture exists yet. The entire tracked tree is:

- `README.md` — entry point (1 line: `# awesome-uconsole`)
- `LICENSE` — GPL-3.0 full text

There are no modules, no data flow, and no code paths. Content that appears to be code (e.g., the `local_cache/` embedding model) is **untracked** tooling residue, not project code.

## Key Directories

- `/` (repo root) — the whole project; tracked files are `README.md` and `LICENSE` only.
- `local_cache/` — **untracked** ~127 MB embedding-model cache from the codebase-memory indexer: an ONNX copy of `BAAI/bge-small-en-v1.5` (384 hidden size, 12-layer BERT, 12 heads, fp32, max 512 positions). ONNX Runtime CPU-only config. Do not commit, read as project content, or use as context; add `local_cache/` to `.gitignore` when first creating it.

## Development Commands

None exist — no package manifest, no Makefile, no task runner. The only verifiable commands:

```sh
git log --oneline        # history: single "Initial commit"
git ls-files             # tracked: README.md, LICENSE
```

When the first real tooling lands, record its commands here.

## Code Conventions & Common Patterns

No conventions are established yet. For an awesome-list repo, apply the standard awesome-list conventions when content is added:

- One section per topic (`## …`), alphabetized entries, `- [Name](url) — description` bullet format.
- Keep `README.md` the single content file; no build step.

For any code added later: GPL-3.0 requires derivative works to carry the same license — add a license header and note it here.

## Important Files

- `README.md` — the project's only content and entry point.
- `LICENSE` — GPL-3.0 v3, 2007 FSF text. All contributions fall under it. (No copyright holder line filled in yet.)

## Runtime/Tooling Preferences

No runtime, package manager, or toolchain is mandated (nothing to run). Do not introduce one until real content requires it; when it does, prefer a standard, boring choice and document it in this section.

`local_cache/fast-bge-small-en-v1.5/` targets ONNX Runtime on CPU, but that reflects the indexer that cached it, not this project.

## Testing & QA

No tests, CI, linters, or QA tooling exist; `.github/` does not exist. The only meaningful check for a Markdown-only repo is link validation — add it (e.g., a link-checker CI job) once the list has actual links.