---
name: grill-with-docs
description: Grilling session that challenges your plan against the existing domain model, sharpens terminology, and updates documentation (CONTEXT.md, ADRs) inline as decisions crystallise. Use when user wants to stress-test a plan against their project's language and documented decisions.
stage: discovery
triggers: []
studio: [agent]
produces: report
effects: workspace
version: 0
---

> Adapted from `mattpocock-skills` `productivity/grilling` (plugin v1.2.3), combined with
> `engineering/domain-modeling` for the CONTEXT.md/ADR habit below. Substituted: upstream quizzes
> the user directly in the conversation, one question then the next; here a round is asked
> through the ask tool as **one call** — the whole frontier as a single numbered "text" ask — and
> the reply comes back through the question channel the same way any parked node's does. The
> frontier/rounds mechanics themselves are otherwise unchanged from upstream.

Interrogate the request relentlessly until you reach a shared understanding. Map it as a
**design tree**: every decision branches into the decisions that hang off it.

Work the tree in **rounds**. The **frontier** is every decision whose prerequisites are already
settled — the questions you can ask _now_ without guessing at answers you have not heard yet. Ask
the whole frontier in **one round, in a single call to the ask tool**: a "text" ask whose question
is the whole frontier formatted per the shape below, each question with its recommended answer. Do
not call the ask tool once per question — that is answering one question at a time for twenty
minutes, which is exactly what asking the whole frontier at once replaces. Then wait for the reply
before the next round.

Format each question in the list like so, as its own visually separate block — a blank line
before and after, never run together with the next question:

```
❓ **Q1** - **<question title>**: <question body, might be multiple sentences>

➡️ <your recommended answer>
```

Number questions continuously across the **whole session**, never restarting per round: if Round 1
asked Q1–Q5, Round 2 opens at Q6. A gap in that sequence (Round 3 opening at Q10 when Round 1 ended
at Q5) means questions were composed and never actually asked — that gap is the bug, not a detail.

Each round's answers reshape the tree — settled decisions push the frontier outward and unblock
questions that depended on them. Recompute the frontier and ask the next round. A question whose
answer depends on another question still open in this round belongs to a _later_ round, not this
one.

**An answer settles only the questions it was shown.** A reply — including a blanket one like "I
agree with all your recommendations", "yes to all", or "your call" — settles only the questions that
were on screen in the round it answered. It is not standing permission to answer a later round's
questions yourself, however confidently you can predict the reply, because nobody has seen those
questions yet. Every round whose frontier has at least one question **is asked**, full stop, and is
recorded as settled only once an actual answer to it has come back — never announce a round
"settled" or "fully settled" on the strength of an earlier round's reply. Do not shrink a round to
work around this: the whole frontier still goes out as one ask; the fix is never asking on the
person's behalf, not asking one question at a time.

Finding _facts_ is your job, never the person's. When a frontier question needs a fact from the
environment (the repository, its docs, its tests), find it yourself rather than asking for it —
dispatch a sub-agent to look for it rather than blocking the whole round on your own reading. Don't
block on it: a running exploration is an unsettled prerequisite, so only the questions downstream
of it wait for the sub-agent to report — ask the rest of the frontier now. The _decisions_ are the
person's — put each to them and wait.

The session is done when the frontier is empty — every branch of the design tree visited, nothing
left silently assumed, and every round along the way actually asked and actually answered. That is
the only way to reach the end: an empty frontier, never a guessed answer standing in for one. **Do
not act on it until the user confirms you have reached a shared understanding.** This node
interrogates, records decisions in the project's own `CONTEXT.md` and `docs/adr/`, and hands on a
report — it never writes application source, and implementation belongs to a downstream node. State
in the final report how many rounds were asked, so a silently skipped round is visible without
reading the whole trail.

If a question can be answered by exploring the codebase, explore the codebase instead.

## Domain awareness

During codebase exploration, also look for existing documentation:

### File structure

Most repos have a single context:

```
/
├── CONTEXT.md
├── docs/
│   └── adr/
│       ├── 0001-event-sourced-orders.md
│       └── 0002-postgres-for-write-model.md
└── src/
```

If a `CONTEXT-MAP.md` exists at the root, the repo has multiple contexts. The map points to where each one lives:

```
/
├── CONTEXT-MAP.md
├── docs/
│   └── adr/                          ← system-wide decisions
├── src/
│   ├── ordering/
│   │   ├── CONTEXT.md
│   │   └── docs/adr/                 ← context-specific decisions
│   └── billing/
│       ├── CONTEXT.md
│       └── docs/adr/
```

Create files lazily — only when you have something to write. If no `CONTEXT.md` exists, create one when the first term is resolved. If no `docs/adr/` exists, create it when the first ADR is needed.

## During the session

### Challenge against the glossary

When the user uses a term that conflicts with the existing language in `CONTEXT.md`, call it out immediately. "Your glossary defines 'cancellation' as X, but you seem to mean Y — which is it?"

### Sharpen fuzzy language

When the user uses vague or overloaded terms, propose a precise canonical term. "You're saying 'account' — do you mean the Employee or the User? Those are different things."

### Discuss concrete scenarios

When domain relationships are being discussed, stress-test them with specific scenarios. Invent scenarios that probe edge cases and force the user to be precise about the boundaries between concepts.

### Cross-reference with code

When the user states how something works, check whether the code agrees. If you find a contradiction, surface it: "Your code cancels entire Orders, but you just said partial cancellation is possible — which is right?"

### Update CONTEXT.md inline

When a term is resolved, update `CONTEXT.md` right there. Don't batch these up — capture them as they happen. "Resolved" means the person's answer to that specific question has actually arrived — never a recommendation you gave that nobody has confirmed yet, however likely it seemed to hold.

`CONTEXT.md` should be totally devoid of implementation details. Do not treat it as a spec, a scratch pad, or a repository for implementation decisions. It is a glossary and nothing else.

### Offer ADRs sparingly

Only offer to create an ADR when all three are true:

1. **Hard to reverse** — the cost of changing your mind later is meaningful
2. **Surprising without context** — a future reader will wonder "why did they do it this way?"
3. **The result of a real trade-off** — there were genuine alternatives and you picked one for specific reasons

If any of the three is missing, skip the ADR.

ADRs live in `docs/adr/` and use sequential numbering: `0001-slug.md`, `0002-slug.md`, etc. Create the `docs/adr/` directory lazily — only when the first ADR is needed.

### ADR format

```
# {Short title of the decision}

{1-3 sentences: what's the context, what did we decide, and why.}
```

That's it. An ADR can be a single paragraph. The value is in recording _that_ a decision was made and _why_ — not in filling out sections.

### CONTEXT.md format

```
# {Context Name}

{One or two sentence description of what this context is and why it exists.}

## Language

**Term**:
{A one or two sentence description of the term.}
_Avoid_: synonym1, synonym2
```

Keep definitions tight — one or two sentences max. Only include terms specific to this project's domain. General programming concepts don't belong.
