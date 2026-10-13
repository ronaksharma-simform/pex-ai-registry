---
name: commit-message-writer
description: Writes a clear git commit message from a diff. Gives a short subject line and a body that explains why the change was made. Use when asked to write or improve a commit message.
metadata:
  version: "1.0.0"
---

# Commit Message Writer

Turn a diff into a commit message a teammate can read in ten seconds.

## Steps

1. **Read the diff.** Look at what changed and why, not only which files.
2. **Write the subject.** Imperative mood, 72 characters or fewer, no full stop.
3. **Write the body.** Explain why the change was needed. Wrap lines at 72 characters.
4. **Check.** Does the subject match the diff? Is anything unrelated mixed in?

## Rules

- One logical change per commit. Say so if the diff holds more than one.
- Never invent a reason the diff does not show. Ask instead.
