# Claude Code Template

A starter repository preconfigured for working with [Claude Code](https://claude.com/claude-code). Use it as a base for new projects so the Claude Code setup, ignore rules, and line-ending normalization are in place from the first commit.

## What's included

| File | Purpose |
|------|---------|
| `.claude/settings.json` | Claude Code settings — `model: opus`, `effortLevel: xhigh`. |
| `.gitignore` | Ignores OS cruft, Python/Node build artifacts, and editor files. |
| `.gitattributes` | Normalizes line endings to LF and marks binary file types. |
| `LICENSE` | Project license. |

## Usage

1. Use this repo as a GitHub template (**Use this template**) or clone it.
2. Remove these template files you don't need and start building your project.
3. Adjust `.claude/settings.json` to taste — see the Claude Code [settings docs](https://docs.claude.com/en/docs/claude-code/settings).

Personal settings that should not be committed belong in `.claude/settings.local.json`, which is already gitignored.

## License

See [LICENSE](LICENSE).
