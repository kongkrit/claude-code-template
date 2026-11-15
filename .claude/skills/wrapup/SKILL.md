---
name: wrapup
description: Write session handoff to .claude/PROGRESS.md and commit
disable-model-invocation: true
allowed-tools: Bash(git add:*), Bash(git commit:*), Bash(git log:*), Bash(git diff:*), Bash(git status:*), Bash(git show:*)
---
Rewrite .claude/PROGRESS.md as a handoff that holds only what changed since the previous handoff, so its git history shows each change once. The one exception: still-open Next steps and Open questions carry over until done or answered.

1. Base: `git log -1 --format=%h -- .claude/PROGRESS.md`, the commit that wrote the previous handoff. Cover `git log <base>..HEAD`, uncommitted changes (`git status`, `git diff HEAD`), and decisions or findings from this session that left no commit.
2. Rewrite .claude/PROGRESS.md: keep the title; the intro line names the base ("Covers the work after `<base>`; earlier handoffs: `git log --follow -p -- .claude/PROGRESS.md`.").
   - What we did: only the work from step 1. Replace the previous list, never append to it.
   - Current state: only what changed since the previous handoff (tests, branch and push state, what became verified or unverified); leave out what still holds.
   - Next steps, Open questions: carry over what is still open word for word, so diffs between handoffs show only real changes; drop what is done or answered, add new items.
3. Stage and commit with a conventional-commit message. That commit becomes the next handoff's base. Do not push.
