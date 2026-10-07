---
name: systematic-debugging
description: 4-phase root cause debugging methodology with 3-fix escalation to prevent infinite fix loops
stage: development
triggers:
  - debug
  - diagnose
  - investigate error
  - root cause
  - why is this failing
  - trace the bug
prerequisites: []
output_format: md
version: 0
---

# Systematic Debugging Skill

## Overview

Enforces a structured 4-phase debugging methodology that prevents the common failure mode of repeatedly guessing at fixes. NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST. After 3 failed fix attempts, the issue is escalated as an architectural problem requiring human design decision.

## The 4-Phase Methodology (MANDATORY)

### Phase 1: OBSERVE

1. Reproduce the error exactly — get the exact error message, stack trace, and failing output
2. Identify the precise input that triggers the failure
3. Determine when it last worked (if applicable)
4. Capture the state: log output, variable values, network responses
5. Document: "The system does X when it should do Y"

### Phase 2: HYPOTHESIZE

1. Form 1-3 SPECIFIC hypotheses about the root cause (not symptoms)
2. Each hypothesis must be falsifiable — you must be able to prove it wrong
3. Rank hypotheses by likelihood
4. Do NOT skip to fixing — hypotheses are not fix attempts

### Phase 3: TEST

1. For each hypothesis, design a minimal test that proves or disproves it
2. Start with the most likely hypothesis
3. Add logging, breakpoints, or assertions to verify
4. Run the test — does it confirm or disprove the hypothesis?
5. If disproved, move to the next hypothesis
6. If all hypotheses are disproved, return to OBSERVE with new data

### Phase 4: CONCLUDE

1. Identify the confirmed root cause
2. Design a fix that addresses the root cause, not the symptom
3. Write a test that would have caught this bug (regression prevention)
4. Apply the fix
5. Verify the fix by running the original reproduction steps + the new test

## The 3-Fix Escalation Rule

Track fix attempts for each issue:

- **Attempt 1**: Apply fix based on confirmed hypothesis → verify → if fails, return to OBSERVE
- **Attempt 2**: Re-investigate with expanded scope → new hypotheses → fix → verify → if fails, widen investigation
- **Attempt 3**: Final attempt with broadest investigation scope → if this fails → ESCALATE

### On Escalation (after 3 failed fixes):

1. STOP all fix attempts immediately
2. Re-frame the problem as ARCHITECTURAL, not a bug
3. Document: what was tried, why each fix failed, what the pattern suggests
4. Present the analysis to the user with a recommendation:
   - "This appears to be a design issue, not a bug. The root cause may be in [architectural decision]. Recommend [approach]."

## Quality Gates

- [ ] Error reproduced with exact steps before any investigation
- [ ] At least 2 hypotheses formed before first fix attempt
- [ ] Each hypothesis tested individually (not bundled with fixes)
- [ ] Root cause confirmed before fix applied
- [ ] Regression test written for the bug
- [ ] Fix verified with original reproduction steps
- [ ] Fix attempt count tracked (max 3 before escalation)

## Anti-Rationalization Defense

| Rationalization                                                        | Why It Is Wrong                                                                          | Required Behavior                                       |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------- |
| "I can see the bug, no need to investigate"                            | Visual inspection misses 70% of root causes. What you see is the symptom, not the cause. | Complete all 4 phases                                   |
| "Let me just try this quick fix"                                       | Untested fixes introduce new bugs 40% of the time.                                       | Form a hypothesis first                                 |
| "The fix worked for a similar bug before"                              | Similar symptoms can have completely different root causes.                              | Test the hypothesis for THIS specific bug               |
| "It's probably just a typo/config issue"                               | "Probably" is not a hypothesis. Be specific and falsifiable.                             | State exactly what the typo/config issue is and test it |
| "I've been debugging this for a while, let me just try one more thing" | This is fix attempt #4+. Escalate.                                                       | Stop after 3 failed fixes and escalate                  |
| "The bug is intermittent, hard to reproduce"                           | Intermittent bugs have specific triggers. Identify the state conditions.                 | Reproduce reliably before investigating                 |
| "It works on my local, must be an environment issue"                   | Environment differences ARE the root cause. Investigate them.                            | Compare environments systematically                     |

## Output Format

Save debugging report as `{ProjectName}_Debug_Report_{IssueKey}_v{Version}.md` in the outputs directory.
