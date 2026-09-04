---
name: New Day
description: Add a daily update entry and confirmation dialog to the sample site.
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
engine: copilot
tools:
  edit: true
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day Agent

Use the UTC date of this workflow run, calculated with `date -u`, as the date
for today's update. Convert it to the existing human-readable wording used by
the page, such as `1st of August`, including the correct ordinal suffix and
full month name.

Read `index.html` and inspect its existing Daily Updates navigation and dialog
markup before editing. If the UTC date is already represented anywhere in the
Daily Updates navigation or in a matching dialog, do not change the file and
call `noop` with a brief explanation.

When the date is absent, edit only `index.html`:

1. Add one navigation `<li>` to the existing `daily-updates-list` with the
   same button structure, classes, attributes, arrow, date wording, and ID
   conventions as the existing entry. Use a unique dialog ID based on the
   date, and make `aria-controls` reference it.
2. Add one matching `<dialog>` using the existing
   `daily-update-dialog`/`daily-update-dialog-content` structure and the same
   accessible `aria-labelledby` and `aria-describedby` pattern. Its header
   must use the same `Daily Update / <date wording>` format, and its content
   must clearly confirm that the daily update ran on the workflow's UTC date.
3. Preserve every existing daily update, including the August 1 entry. Do not
   change `styles.css`, the page's script, or unrelated HTML.

Check that the new button's `aria-controls` points to the new dialog and that
the dialog's IDs are unique. If an edit was made, create exactly one pull
request using the safe `create_pull_request` output, describing the date added
and the confirmation dialog. If no edit was needed, use `noop` instead.