---
name: slack-post
description: Post project updates, artifact summaries, and status notifications to Slack channels
stage: delivery
triggers:
  - post to slack
  - share in slack
  - send to slack
  - slack message
  - notify slack
  - post summary to slack
prerequisites: []
output_format: md
version: 0
---

## Overview

The Slack Post skill enables the delivery agent to share project updates, artifact summaries, and status notifications directly to configured Slack channels using MCP Slack tools.

## Workflow

1. **Identify Target Channel**: Determine the Slack channel from project configuration or user prompt
2. **Compose Message**: Build a concise, well-formatted summary of the project status or specified artifact
3. **Post to Slack**: Send the message using available Slack MCP tools
4. **Confirm Delivery**: Report success or failure back to the user

## Output

A confirmation message with the Slack channel and message permalink.

## Quality Gates

- Message must be concise and well-formatted (markdown)
- Channel must be verified before posting
- Sensitive data (API keys, credentials) must never be included in Slack messages
