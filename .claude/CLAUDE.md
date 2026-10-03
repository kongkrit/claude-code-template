# CLAUDE.md

Guidance for Claude Code in this repository.

## What this is

A **Claude Code template** — a starting point for new projects, not an application. It holds only configuration and licensing files; application code gets added alongside them.

## Code principles — IMPORTANT

**All code MUST be SIMPLE, MINIMAL, EASY TO UNDERSTAND, and DRY.** These rules come before cleverness, speculative flexibility, and personal style.

- **Simple:** use the most straightforward approach that works. No clever tricks, premature abstraction, or premature optimization.
- **Minimal:** write only what the task needs. No speculative features, unused options, or "just in case" code. Fewer lines, files, and dependencies win. Delete dead code.
- **Easy to understand:** a newcomer should follow it on first read. Clear names, small functions, shallow nesting, obvious control flow.
- **DRY:** one source of truth for each piece of logic, data, and config. Search for existing code to reuse before writing new code; never copy-paste logic. Extract it once instead.
- **When in doubt, choose the simpler option.** Before finishing, re-read your diff and cut anything that isn't needed.

## How to explain things

These rules apply to explanations to the user and to code comments, not to commit messages.

For code comments:
- Explain why and the mechanism; don't restate what the code plainly does.
- Define a term once, at its first use in the file.
- Add a worked numeric example only for non-obvious math (scaling, units, bit layouts).
- Keep comments as short as the point allows; "Simple", "Minimal", "Easy to understand", and "DRY" still applies.

Audience: someone with a BS in EE who remembers the fundamentals (circuits, signals, calculus, basic probability and statistics) but not every formula or every field's jargon. Write for a sharp engineer outside the specialty.

Goal: as simple as possible, without saying anything false.

1. Start with the plain-language answer in 1-2 sentences, then the reasoning.
2. Explain the mechanism (what causes what) in words before any math.
3. Define each technical term the first time it appears, in a short phrase. Introduce as few new terms as possible.
4. Use an equation only when it makes the point clearer than words. If you use one, define every symbol and show one worked example with real numbers.
5. Prefer a concrete numeric example over abstract notation.
6. Use an analogy (EE analogies are welcome) only if it maps accurately, and say where it breaks down.
7. When you simplify, say what you left out and when it would matter.
8. No handwaving: back each claim with a reason, a number, or a source. If the answer depends on something, say what. If unsure, say so.
9. Before sending, check: could I follow this on the first read without looking anything up? If not, rewrite it.

## Layout

- `.claude/settings.json` — committed settings (`model: opus`, `effortLevel: xhigh`), permission allowlist, and a `SessionStart` hook that prints `PROGRESS.md` into context. Personal overrides go in the gitignored `.claude/settings.local.json`, never here.
- `.claude/commands/wrapup.md` — `/wrapup`: writes a session handoff to `PROGRESS.md`, then commits.
- `PROGRESS.md` — session handoff maintained by `/wrapup`.
- `.gitignore`, `.gitattributes` — ignore rules; LF line endings and binary file types.
- `README.md`, `LICENSE` — human-facing overview and license.

## Conventions

- LF line endings everywhere; never introduce CRLF.
- New languages or toolchains extend `.gitignore` and `.gitattributes` — no parallel ignore files. Keep new entries consistent with existing ones.
- Respect the [LICENSE](../LICENSE) when adding dependencies.
- As the template becomes a real project, add build, test, and run commands here.

## Development environment

- **Debian 13 (trixie)** with `docker` installed. Base tooling via `apt`: `git`, `gh`, `python3`, `python3-venv`, `python3-pip`, `python3-dev`, `build-essential`, `curl`, `jq`; plus `uv` from its standalone installer into `~/.local/bin` (commands in the [README](../README.md#development-setup-debian-13)).
- **Install missing tools yourself:** `sudo apt install -y <package>` (`sudo apt update` first if not found). Use `apt` for system tools only. If the project will keep relying on a new tool, add it to the README's install command.
- **Never `pip install` system-wide** (PEP 668). Use a per-project venv:

  ```bash
  uv venv && uv pip install -r requirements.txt    # or: uv sync
  # or: python3 -m venv .venv && source .venv/bin/activate && pip install -r requirements.txt
  ```
- `node`/`npm` and .NET are not used; serve static content with `python3 -m http.server`. Multi-arch Docker builds need a one-time QEMU + buildx setup (see README).
