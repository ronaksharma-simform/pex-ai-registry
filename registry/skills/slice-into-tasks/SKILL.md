---
name: slice-into-tasks
description: Break a spec or plan into a list of vertical-slice tasks, ordered blockers-first, ready for a Loop node to run one at a time.
stage: estimation
triggers: []
studio: [to-tasks]
produces: worklist
effects: read-only
version: 0
---

> Adapted from `mattpocock-skills` `engineering/to-tickets` (plugin v1.2.3). Substituted: upstream
> publishes tickets to an issue tracker and quizzes the user on the breakdown, iterating until
> they approve it; here the node hands the list on as a `worklist` envelope, and the engine's own
> approval checkbox is where a person sends the list back with a reason instead of upstream's
> quiz-and-iterate loop. Upstream's blocking-edges idea now has a home: a worklist item's own
> `dependsOn` field names the ids of the items that block it (ticket 07), and the Loop node starts
> only an item whose blockers have already succeeded. This Skill still orders the list blockers
> first, which is now the tiebreak among items that become ready at the same time rather than the
> only mechanism a dependency can be honoured by. The vertical-slice rules and the expand–contract
> sequence below are ported verbatim — they are the value, not the scaffolding — with one word
> substituted throughout: upstream's "ticket" reads "item" here, the unit this Skill hands on.

Break the work the hand-offs describe into items — tracer-bullet vertical slices, each small
enough for one agent to finish on its own.

<vertical-slice-rules>

- Each slice cuts a narrow but COMPLETE path through every layer (schema, API, UI, tests) —
  vertical, NOT a horizontal slice of one layer
- A completed slice is demoable or verifiable on its own
- Each slice is sized to fit in a single fresh context window
- Any prefactoring should be done first

</vertical-slice-rules>

**Wide refactors are the exception to vertical slicing.** A **wide refactor** is one mechanical
change — rename a column, retype a shared symbol — whose **blast radius** fans across the whole
codebase, so a single edit breaks thousands of call sites at once and no vertical slice can land
green. Don't force it into a tracer bullet; sequence it as **expand–contract**. First expand: add
the new form beside the old so nothing breaks. Then migrate the call sites over in batches sized
by blast radius (per package, per directory), each batch its own item blocked by the expand,
keeping CI green batch to batch because the old form still exists. Finally contract: delete the
old form once no caller remains, in an item blocked by every migrate batch. When even the batches
can't stay green alone, keep the sequence but let them share an integration branch that all block
a final integrate-and-verify item — green is promised only there.

## Ordering and dependencies

Declare a real dependency in `dependsOn`: the list of item ids that must succeed before this one
starts. The Loop node schedules from that field directly — it starts every item whose blockers
have all succeeded, up to its configured width, and releases a dependent the moment its blocker
finishes, so independent items still run side by side. Leave `dependsOn` empty or omit it for an
item with no blocker.

Still order the list **blockers first** — an item with no blockers comes before anything that
needs it. The Loop node no longer needs that order to honour a dependency, but it is still the
tiebreak among items that become ready at the same moment, and it keeps the list readable.

Look for opportunities to prefactor the code to make the implementation easier first: "make the
change easy, then make the easy change." Explore the repository if you have not already, and use
its own domain vocabulary in every item's title and description — name real files and commands
that actually exist in this project.
