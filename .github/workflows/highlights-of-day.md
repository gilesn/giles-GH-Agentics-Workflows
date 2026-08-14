---
engine: copilot
name: Highlights of the Day
description: Add an unused GitHub Agentic Workflows FAQ highlight to the daily update.
on:
  schedule: every 6 hours
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
  web-fetch: {}
network:
  allowed:
    - github.github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# Highlights of the Day

## Task

Use the workflow run's current UTC date, obtained at runtime with a UTC-aware
command such as `date -u`. Fetch the GitHub Agentic Workflows FAQ from:

https://github.github.com/gh-aw/reference/faq/

Review every FAQ question and answer on that page, then compare them with all
existing questions and answers in `index.html`. Select exactly one FAQ that is
not already represented in the HTML. Do not invent an FAQ or claim that a FAQ is
new when its question or answer is already represented.

Before editing, inspect every existing Daily Updates navigation control and
dialog. Never duplicate a date, navigation control, dialog, FAQ question, or
FAQ answer. If the current UTC date's dialog already contains an FAQ, or if no
unused FAQ remains, make no change and call `noop` with a brief explanation.

When an unused FAQ is available:

1. Format the UTC date as an ordinal day and full month in visible text, such as
   `1st of August`. Use the existing lowercase month-day slug convention for
   IDs, such as `august-1-dialog`, `august-1-question`, and
   `august-1-answer`.
2. If a dialog for today's UTC date already exists and is an obvious placeholder,
   reuse it by replacing its placeholder question and answer with the selected
   FAQ. Otherwise add one matching navigation control to the existing Daily
   Updates list and one matching accessible dialog.
3. Follow the existing HTML structure and styling exactly. Navigation controls
   must use `class="daily-update-trigger"`, `aria-haspopup="dialog"`, a matching
   `aria-controls`, and `data-dialog-trigger`. Dialogs must use
   `class="daily-update-dialog"`, matching `aria-labelledby` and
   `aria-describedby` IDs, the existing header and close form, and concise
   visible wording.
4. Put the selected FAQ question in the question heading and a concise,
   accurate answer based on the official FAQ in the answer paragraph. Preserve
   the existing HTML entities and accessible close-button pattern where they
   apply.

Preserve every existing Daily Updates entry and all existing page behavior. Do
not modify `styles.css`, the inline dialog script, or any file other than
`index.html`. Do not add a second script.

If an edit is needed, create at most one pull request using the configured
`create-pull-request` safe output. The pull request must contain only
`index.html`. If no edit is needed, use `noop` instead.