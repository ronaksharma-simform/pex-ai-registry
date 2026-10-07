---
name: review-standards
description: Review the changes in this run's folder against this repository's documented coding standards, plus a fixed baseline of Fowler code smells. Reports findings; changes nothing.
stage: qa
triggers: []
studio: [agent]
produces: report
effects: read-only
version: 0
---

> Adapted from the Standards axis of `mattpocock-skills` `engineering/code-review` (plugin
> v1.2.3). Substituted: upstream asks the user for a fixed point (a commit, branch or tag) and
> diffs `HEAD` against it, then hands its findings to an aggregating step that also runs a
> parallel Spec sub-agent; here there is no user to ask mid-run and no sub-agent — this is a
> single node whose only axis is Standards, and the Spec axis is a separate Skill on a separate
> node, joined by an arrow rather than fanned out inside this one (a sub-agent's steps never
> become trail rows, its cost arrives as one opaque number, and nothing a person types can steer
> it). The fixed point is derived rather than asked for: diff the run's branch against its base.
> The code-smell baseline below is ported verbatim — it is the value, not the scaffolding.

Review the changes made in this run's folder. You report findings; you do not change anything.

## Find the diff

Diff the current branch against its base (the commit the branch forked from, or the repository's
default branch if that is not available) — `git diff` and `git log` against that point, not
against the working tree alone. If the hand-offs above name a branch or the files that changed,
start there.

## Check against the repository's own standards

Look for anything in the repository that documents how code should be written here — a
`CLAUDE.md`, `CONTEXT.md`, `CODING_STANDARDS.md`, `CONTRIBUTING.md`, or equivalent. A documented
repository standard always wins: where it endorses something the baseline below would otherwise
flag, suppress the flag.

## Check against the baseline

On top of whatever the repository documents, always check the diff against this fixed set of
Fowler code smells (_Refactoring_, ch. 3). Each is a labelled judgement call, never a hard
violation, and skip anything tooling already enforces (a linter, a type checker):

- **Mysterious Name** — a function, variable, or type whose name doesn't reveal what it does or
  holds. → rename it; if no honest name comes, the design's murky.
- **Duplicated Code** — the same logic shape appears in more than one hunk or file in the change.
  → extract the shared shape, call it from both.
- **Feature Envy** — a method that reaches into another object's data more than its own. → move
  the method onto the data it envies.
- **Data Clumps** — the same few fields or params keep travelling together (a type wanting to be
  born). → bundle them into one type, pass that.
- **Primitive Obsession** — a primitive or string standing in for a domain concept that deserves
  its own type. → give the concept its own small type.
- **Repeated Switches** — the same `switch`/`if`-cascade on the same type recurs across the
  change. → replace with polymorphism, or one map both sites share.
- **Shotgun Surgery** — one logical change forces scattered edits across many files in the diff. →
  gather what changes together into one module.
- **Divergent Change** — one file or module is edited for several unrelated reasons. → split so
  each module changes for one reason.
- **Speculative Generality** — abstraction, parameters, or hooks added for needs the spec doesn't
  have. → delete it; inline back until a real need shows.
- **Message Chains** — long `a.b().c().d()` navigation the caller shouldn't depend on. → hide the
  walk behind one method on the first object.
- **Middle Man** — a class or function that mostly just delegates onward. → cut it, call the real
  target direct.
- **Refused Bequest** — a subclass or implementer that ignores or overrides most of what it
  inherits. → drop the inheritance, use composition.

## Report

For each finding, cite the standard it breaks (file and rule) or name the smell and quote the
hunk. Distinguish hard violations of a documented standard from judgement calls on the baseline —
the baseline is always advisory, a documented standard can be a hard violation.

Hand on the findings and a count by severity. You do not fix anything here — a later node, or a
person reading your report, decides what to change.
