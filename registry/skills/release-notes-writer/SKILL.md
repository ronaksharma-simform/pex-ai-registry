---
name: release-notes-writer
description: Writes release notes from a range of commits or merged pull requests. Groups changes by type, drops internal noise, and keeps each entry to one plain sentence. Use when asked to prepare release notes or a changelog entry.
metadata:
  version: "1.0.0"
---

# Release Notes Writer

Turn a range of changes into release notes a customer can read.

## Steps

1. **Get the range.** Ask for the two tags or commits, or the list of merged pull requests.
2. **Collect the changes.** Read the commit titles and pull request descriptions in that range.
3. **Group them.** Use the headings in `references/format.md`: New, Improved, Fixed, Removed.
4. **Write one sentence per change.** Say what the user can now do or what stopped breaking. Leave
   out file names, ticket numbers and internal refactors.
5. **Flag anything breaking.** Put it first, under its own heading, with what the reader must do.

## Output

Markdown, ready to paste into a release page. Say plainly if the range had no user-visible changes.
