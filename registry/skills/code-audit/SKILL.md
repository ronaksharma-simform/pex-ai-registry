---
name: code-audit
description: Perform comprehensive code quality audits covering style, documentation, error handling, testing, dependencies, security, and performance
stage: qa
triggers:
  - code audit
  - code review
  - audit the code
  - code quality
  - review the codebase
  - quality audit
  - security audit
  - audit this
prerequisites: []
output_format: docx
version: 0
---

# Code Audit Skill

## Overview

Performs a comprehensive code quality audit across 8 dimensions: code style and formatting, documentation, error handling, testing, dependencies management, code organization, performance considerations, and security practices. Generates a structured audit report with severity-prioritized findings and an actionable recommendations roadmap.

## Prerequisites

- Access to the project codebase via git workspace or scaffold artifacts.
- Read solution design and architecture decisions for context-aware analysis.

## Workflow

1. Analyze project structure and identify key files for review
2. Evaluate code style and formatting (PEP 8 / ESLint compliance, naming conventions)
3. Assess documentation quality (docstrings, comments, type hints, README)
4. Review error handling practices (exception handling, logging, defensive programming)
5. Evaluate test coverage and organization (unit, integration, functional tests)
6. Check dependencies management (version pinning, security, virtual environments)
7. Analyze code organization (module structure, separation of concerns, reusability)
8. Identify performance issues (algorithmic efficiency, memory usage, I/O optimization)
9. Audit security practices (input validation, secrets management, OWASP top 10)
10. Prioritize findings by severity and generate recommendations roadmap
11. Save audit report as markdown and docx artifacts

## Reference Files

- `references/audit-checklist.md` — Standard audit checklist by category

## Quality Gates

- [ ] Executive summary with critical issues highlighted
- [ ] All 8 audit dimensions covered with specific findings
- [ ] Code examples included for each identified issue
- [ ] Findings prioritized by severity (critical, high, medium, low)
- [ ] Actionable recommendations with clear next steps
- [ ] Recommendations roadmap ordered by priority and effort
- [ ] No false positives — findings reference actual code patterns

## Anti-Rationalization Defense

The agent MUST NOT downplay findings or skip audit dimensions. Below are common rationalizations and why they are wrong:

| Rationalization                                      | Why It Is Wrong                                                                                           | Required Behavior                                                   |
| ---------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| "The code is well-structured, no major issues"       | Every codebase has issues. A clean audit report means the audit was superficial.                          | Dig deeper — check error handling, edge cases, security boundaries  |
| "Security isn't a concern for internal tools"        | Internal tools get compromised via lateral movement. 34% of breaches start from internal systems.         | Audit OWASP top 10 regardless of deployment context                 |
| "This is a prototype, quality standards don't apply" | Prototypes become production code. Technical debt from prototypes is the hardest to remove.               | Apply full audit standards; flag prototype-quality code as findings |
| "The team knows about this issue already"            | Known issues that aren't tracked get forgotten. The audit report IS the tracking mechanism.               | Document every finding regardless of team awareness                 |
| "This finding is low severity, not worth reporting"  | Low-severity issues compound. Ten low-severity issues equal one high-severity architectural problem.      | Report all findings with severity classification                    |
| "The dependency versions are fine"                   | Outdated dependencies accumulate CVEs. One unpatched library can compromise the entire system.            | Check every dependency against known vulnerability databases        |
| "Error handling is adequate"                         | Swallowed exceptions, generic catches, and missing error boundaries are the #1 source of silent failures. | Verify specific, actionable error handling at every system boundary |

## Output Format

Save as `{ProjectName}_Code_Audit_Report_v{Version}.docx` in the outputs directory.
