---
name: implement-the-work
description: Implement a piece of work test-first, from a spec, plan or a worklist item — the process an Implement node follows.
stage: development
triggers: []
studio: [implement]
produces: codechange
effects: workspace
version: 0
---

> Adapted from `mattpocock-skills` `engineering/implement` (plugin v1.2.3), combined with
> `engineering/tdd` (same plugin, same v1.2.3) for the test-first habit inlined below. Substituted: upstream ends by invoking
> `/code-review`; here that is not this Skill's job at all — it is an arrow a person draws from
> this node to a review node on the canvas, not an instruction this Skill gives itself. Upstream
> also says "commit your work to the current branch" and "open a pull request" is implied by the
> review-then-ship flow it assumes; here neither is this Skill's to ask for; the node's own system
> prompt already states the folder is committed for it and forbids publishing whatever a Skill's
> prose says, so this body does not repeat or contradict either rule.

Implement the work described by the hand-offs above — a spec, a plan, or a single worklist item —
in the folder you were started in.

## Work test-first

Default to red before green: write the failing test first, then only enough code to pass it. Work
in **vertical slices** — one seam, one test, one minimal implementation, repeat — rather than
writing a batch of tests up front and then a batch of implementation. Each slice is a tracer
bullet that responds to what the last cycle taught you, not a guess at the whole shape in advance.

Test only at seams the hand-offs already name or that are obvious from the code you are changing —
a public interface, not an internal collaborator. A good test reads like a specification of a
capability ("user can check out with a valid cart") and survives a refactor because it does not
care about internal structure. Two failure shapes to avoid:

- **Implementation-coupled** — mocking an internal collaborator, testing a private method, or
  checking a side channel (querying the database directly instead of going through the interface
  under test). The tell: the test breaks on a refactor even though behaviour did not change.
- **Tautological** — the assertion recomputes the expected value the same way the code does, so it
  passes by construction. The expected value must come from an independent source of truth: a
  known-good literal, a worked example, the spec itself.

Refactoring is not part of the red-green loop. Land the passing test and the minimal
implementation first; clean up in a following slice once green.

## Verifying before you hand on

Run typechecking and the single test file you are working against regularly through the loop, and
run the full test suite once before you finish. Do not hand your work on with a red suite.

## What this node does not do

Work only inside the folder you were started in. Do not push, do not open a pull request, and do
not merge anything — publishing is a different node's job, later on the canvas, whatever this
Skill's prose says about it. Committing as you go is fine but not required.

Finish by saying, in a few sentences, what you changed and why — that is the only thing the next
node sees.
