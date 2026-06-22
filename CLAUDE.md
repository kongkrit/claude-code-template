# CLAUDE.md

Guidance for Claude Code when working in this repository.

## What this is

This is a **Claude Code template repository** — a starting point for new projects, not an application itself. It currently contains only configuration and licensing files. When this template is used for a real project, expect application code to be added alongside the files below.

## Repository layout

- `.claude/settings.json` — Claude Code settings committed for the project (`model: opus`, `effortLevel: xhigh`). Personal overrides go in `.claude/settings.local.json` (gitignored), never in the committed file.
- `.gitignore` — ignores OS cruft, Python/Node build artifacts, and editor files.
- `.gitattributes` — enforces LF line endings and marks binary file types. Keep new text/binary file types consistent with the existing entries.
- `LICENSE` — the project license.
- `README.md` — human-facing overview of the template.

## Conventions

- Line endings are LF across the repo (enforced by `.gitattributes`). Do not introduce CRLF.
- When adding a new language or toolchain, extend `.gitignore` and `.gitattributes` rather than creating parallel ignore files.
- Respect the project [LICENSE](LICENSE) when adding dependencies.

## Notes

- As the template grows into a real project, update this file with build, test, and run commands so they are discoverable.
