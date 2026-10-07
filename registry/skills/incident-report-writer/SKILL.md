---
name: incident-report-writer
description: Writes a blameless incident report from a timeline, logs and chat excerpts. Separates what happened, the impact, the cause and the follow-up actions. Use when asked to write up an outage or a post-incident review.
metadata:
  version: "1.0.0"
---

# Incident Report Writer

Turn raw incident material into a report a new team member can follow.

## Steps

1. **Collect the material.** Ask for the timeline, the alerts, the relevant logs and the chat excerpts.
2. **Build the timeline.** One line per event, in time order, with the time zone stated once.
3. **State the impact.** Who was affected, for how long, and how many requests or users, if known.
4. **Find the cause.** Use the five whys in `references/template.md`. Stop at a cause the team can change.
5. **List follow-up actions.** Each has an owner and a date. Mark which ones prevent a repeat.

## Rules

- Blameless. Describe what the system and the process allowed, never who made the mistake.
- Say plainly what is not known yet instead of guessing.
