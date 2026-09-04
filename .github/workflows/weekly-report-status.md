---
name: Weekly Report Status
description: Publish a concise weekly activity report for the repository.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
engine: copilot
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Generate a concise activity report for the previous seven full days ending at
workflow start time in UTC. Review repository commits, issues, and pull
requests from that window using the available GitHub read tools.

Create exactly one issue containing the report. Use `###` headings for report
sections and include the report window, a brief summary, and concise counts and
details for commits, issues, and pull requests. Clearly state when no activity
occurred in the reporting window. Do not invent activity or classifications.

If there was no activity of any kind, still create the issue and clearly state
that no commits, issues, or pull requests occurred during the window.