---
engine: copilot
description: Publish a concise weekly repository activity report.
on:
  schedule:
    - cron: "0 9 * * 1"
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
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

## Task

Create a concise GitHub-flavored Markdown activity report for the previous seven
full days ending at the workflow start time in UTC. Use the GitHub tools to review
repository commits, issues, and pull requests from that window.

The report must:

- Summarize commit activity, including the number of commits and notable changes.
- Summarize issues opened or updated, including relevant titles and statuses.
- Summarize pull requests opened, merged, or updated, including relevant titles and statuses.
- State clearly that no activity occurred when the seven-day window contains no commits, issue activity, or pull request activity.
- Use `###` headings for report sections and keep the report concise.
- Include the UTC reporting window in the report.

Publish the report as one new issue using the configured `create-issue` safe output.
Use a meaningful title after the `[weekly-report] ` prefix and a body of at least 20
characters. Do not make direct repository writes. If no report issue should be
created, call `noop` with a brief explanation and the evaluated UTC window.

## Safe Outputs

- Use only `create-issue` for publishing the report.
- Use `noop` when there is no activity or no visible change is needed.