---
name: write-the-spec
description: Turn a settled request into a written spec — synthesis of what has already been discussed and grilled, not another interview.
stage: discovery
triggers: []
studio: [agent]
produces: spec
effects: read-only
version: 0
---

> Adapted from `mattpocock-skills` `engineering/to-spec` (plugin v1.2.3). Substituted: upstream
> publishes the finished spec to the project's issue tracker and applies a triage label there;
> here the node hands the spec on as an envelope, and whatever a person put after this node on
> the canvas decides what happens to it next. The section list below is ported verbatim — it is
> the value, not the scaffolding.

This node's job is synthesis, not another interview: turn what the hand-offs above already
settled into a written spec. Do not ask questions here — if the request is still unsettled, that
is a grilling node's job, upstream of this one.

## Process

1. Read the hand-offs and the repository. Use the project's own domain vocabulary throughout, and
   respect any decisions the repository already records (its glossary, its ADRs).
2. Sketch out the seams at which the feature will be tested. Prefer existing seams to new ones,
   and the highest seam possible — the fewer seams, the better, and one is the ideal.
3. Write the spec using the template below.

<spec-template>

## Problem Statement

The problem the user is facing, from the user's perspective.

## Solution

The solution to the problem, from the user's perspective.

## User Stories

A LONG, numbered list of user stories. Each user story should be in the format of:

1. As an <actor>, I want a <feature>, so that <benefit>

<user-story-example>
1. As a mobile bank customer, I want to see balance on my accounts, so that I can make better informed decisions about my spending
</user-story-example>

This list of user stories should be extremely extensive and cover all aspects of the feature.

## Implementation Decisions

A list of implementation decisions that were made. This can include:

- The modules that will be built/modified
- The interfaces of those modules that will be modified
- Technical clarifications from the developer
- Architectural decisions
- Schema changes
- API contracts
- Specific interactions

Do NOT include specific file paths or code snippets. They may end up being outdated very quickly.

Exception: if a prototype produced a snippet that encodes a decision more precisely than prose can (state machine, reducer, schema, type shape), inline it within the relevant decision and note briefly that it came from a prototype. Trim to the decision-rich parts — not a working demo, just the important bits.

## Testing Decisions

A list of testing decisions that were made. Include:

- A description of what makes a good test (only test external behavior, not implementation details)
- Which modules will be tested
- Prior art for the tests (i.e. similar types of tests in the codebase)

## Out of Scope

A description of the things that are out of scope for this spec.

## Further Notes

Any further notes about the feature.

</spec-template>
