---
engine: copilot
name: New Day
description: Add the current UTC date to the static site's daily updates.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

## Task

Use the workflow run's current UTC date, obtained at runtime with a UTC-aware
command such as `date -u`, to update `index.html`.

Before editing, inspect the existing Daily Updates navigation and every matching
dialog. If the current UTC date is already present anywhere in the existing daily
updates, make no change and call `noop` with a brief explanation. Never duplicate
a date, navigation control, or dialog.

When the date is not present:

1. Add one navigation control to the existing `Daily Updates` list.
2. Add one matching accessible `<dialog>` using the existing structure and ID
   conventions. The navigation control must use `aria-haspopup="dialog"`,
   `aria-controls`, and `data-dialog-trigger`; the dialog must use matching
   `aria-labelledby` and `aria-describedby` IDs.
3. Use the existing date wording and styling conventions: an ordinal day and
   full month in visible text, such as `1st of August`, and a lowercase
   month-day slug for IDs, such as `august-1-dialog`,
   `august-1-question`, and `august-1-answer`.
4. Make the dialog content clearly confirm that the daily update ran on the
   current UTC date. Preserve the existing dialog header, close form, and
   accessible close button pattern.

Preserve every existing daily update and all existing HTML behavior. Do not
modify `styles.css` or any file other than `index.html`. Use the existing inline
dialog script; do not add another script or change the existing script.

If an edit is needed, create at most one pull request with the configured
`create-pull-request` safe output. The pull request must contain only
`index.html`. If no edit is needed, use `noop` instead.