---
name: finding-verification
description: Adversarially re-check another reviewer's findings against the actual code, confirming, refuting, or declining to confirm each one without modifying anything
stage: qa
triggers:
  - verify these findings
  - verify the review findings
  - check the reviewer's findings
  - confirm or refute findings
prerequisites: []
output_format: md
version: 0
---

# Finding Verification Skill

## Overview

Independently judges each finding of one completed code review against the actual code: confirmed
(the failure mechanism was traced), refuted (the claim was shown wrong), or plausible (neither).
Never edits: the owning agent is read-only by capability.

Distinct from `code-review`, which produces findings. This skill judges findings someone else
produced, and exists so an automated review's output is checked before a human reads it.

This file is the registry/routing declaration only: the verification runner builds the verifier's
prompt from the `review-verifier` agent manifest and does not load skill content, so the
operational procedure lives there and this workflow is its summary.

## Workflow

1. Read each finding's file and enough surrounding code to follow the claimed failure end to end
2. Trace the failure in the code, or find the fact that disproves it
3. Submit one verdict per finding id: confirmed, refuted, or plausible
4. Conclude with a one-paragraph summary of what was checked

## Output

One `{findingId, verification, reasoning}` verdict per finding, then a conclusion summary.
