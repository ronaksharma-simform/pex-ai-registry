---
name: review-spec
description: Review the changes in this run's folder against the spec or plan that started the work. Reports findings; changes nothing.
stage: qa
triggers: []
studio: [agent]
produces: report
effects: read-only
version: 0
---

> Adapted from the Spec axis of `mattpocock-skills` `engineering/code-review` (plugin v1.2.3).
> Substituted: upstream looks up the originating issue in a tracker (commit references, a path
> argument, a matching file under `docs/`/`specs/`/`.scratch/`, or asks the user) and runs this
> axis as one of two parallel sub-agents inside a single review step; here the spec is a hand-off
> — an upstream node's `spec` or `plan` envelope — rather than something to go looking for, and
> this axis is its own node rather than a sub-agent, joined to the Standards node by an arrow so
> neither axis can hide the other's findings. If no spec was handed on, say so and report nothing
> further, the same as upstream skipping this axis when it finds no spec.

Review the changes made in this run's folder against the spec or plan the hand-offs above
describe. You report findings; you do not change anything.

If nothing upstream of you handed on a spec or a plan, say so plainly and stop — there is nothing
to check this axis against, and inventing a spec from the diff would be reviewing the code against
itself.

## Find the diff

Diff the current branch against its base (the commit the branch forked from, or the repository's
default branch if that is not available). If the hand-offs name a branch or the files that
changed, start there.

## Check the diff against the spec

Report, quoting the spec line for each finding:

- **Missing or partial** — requirements the spec asked for that the diff does not implement, or
  implements incompletely.
- **Scope creep** — behaviour in the diff that the spec did not ask for.
- **Implemented but wrong** — a requirement that looks addressed but whose implementation does not
  actually satisfy what the spec line describes.

## Report

Hand on the findings and a count by severity. You do not fix anything here — a later node, or a
person reading your report, decides what to change.
