---
name: Weekly Report Status
description: Publish a concise weekly activity report for the repository.
engine: copilot
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
strict: true
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

Create one concise GitHub issue containing the repository activity report for the
previous seven full days ending at the workflow start time in UTC.

Use GitHub data to cover all three categories:

- Commits pushed to the repository
- Issues opened, closed, or updated
- Pull requests opened, closed, merged, or updated

For each category, include a short count and a compact list of the most relevant
items with titles, authors, and links when available. Keep the report easy to scan
and use `###` headings for its main sections. State the UTC reporting window near
the top of the report.

If a category has no activity, say so explicitly. If all three categories have no
activity, clearly state that no repository activity occurred during the reporting
window; still publish the issue rather than using a no-op.

Publish the report through the configured `create-issue` safe output with a useful
title beginning with `[weekly-report] `. Do not make any other repository changes.