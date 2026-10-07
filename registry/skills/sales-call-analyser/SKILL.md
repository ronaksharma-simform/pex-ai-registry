---
name: sales-call-analyser
description: Analyse proposal/sales call transcripts to evaluate customer sentiment, discussion quality, and individual Simform team performance with scoring
stage: discovery
triggers:
  - analyse sales call
  - analyze sales call
  - sales call analysis
  - call transcript analysis
  - proposal call analysis
  - evaluate sales call
  - review sales call
  - sales call review
  - call recording analysis
  - analyse call
  - analyze call
  - call analysis
  - call sentiment
  - sales call score
prerequisites:
  - docx
output_format: docx
version: 0
---

# Sales Call Analyser Skill

## Overview

Analyses proposal/sales call transcripts between Simform team members and customers. Evaluates customer sentiment, discussion quality, and Simform team performance at both the team and individual level. Produces a structured analysis report with actionable coaching feedback and quality scores.

## Prerequisites

- Always read `docx/SKILL.md` first for document formatting guidelines.
- If a SharePoint site is available, use SharePoint tools to locate and download call transcript files.

## Workflow

1. Locate the call transcript — check SharePoint for recordings/transcripts, or use the transcript provided in the prompt
2. Read and parse the full transcript, identifying all speakers and their roles (Simform team vs customer)
3. Analyse overall customer sentiment (Positive/Neutral/Negative) with supporting quotes
4. Evaluate Simform's discussion quality — structure, professionalism, needs-addressed, solutions-mapped, next-steps
5. Perform individual analysis for each Simform speaker — strengths, mistakes, irrelevant questions, missed opportunities
6. Assess relevance and alignment — off-topic diversions, mismatched expectations
7. Calculate quality scores (0–100) for each individual and overall Simform performance
8. Generate improvement suggestions — team-level and individual coaching tips
9. Save the structured analysis report as a .docx artifact

## Reference Files

- `references/analysis-template.md` — Output structure template with section guidance
- `references/scoring-rubric.md` — Scoring criteria and rubric for individual and team evaluation

## Quality Gates

- [ ] All 6 analysis sections present (Sentiment, Discussion Quality, Individual Analysis, Relevance, Scoring, Improvements)
- [ ] Customer sentiment includes specific quotes/evidence from transcript
- [ ] Each Simform speaker individually analysed with strengths and weaknesses
- [ ] Individual scores (0–100) provided for every Simform participant
- [ ] Overall Simform quality score (0–100) with justification
- [ ] Improvement suggestions are specific and actionable, not generic
- [ ] Analysis is objective and based only on transcript content
- [ ] Off-topic or irrelevant discussion points are identified

## Output Format

Save as `{ProjectName}_Sales_Call_Analysis_v{Version}.docx` in the outputs directory.
