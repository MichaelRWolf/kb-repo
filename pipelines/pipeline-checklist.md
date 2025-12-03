# Migration Pipeline Checklist (Confluence → Google Docs)

Short, practical checklist for the migration run.

## Before Migration

- [ ] Confirm Confluence space(s) to migrate.
- [ ] Ensure you have permission to export each space.
- [ ] Create a target folder in Google Drive for each space.
- [ ] Decide folder strategy (default: flat, or reconstruct hierarchy later).

## During Migration

- [ ] Export each Confluence space as **HTML** (always flat — hierarchy in `index.html` only).
- [ ] Verify export directories contain one `*.html` per page.
- [ ] Enable "Convert uploaded files to Google Docs format" in Drive settings.
- [ ] Upload export folder(s) into the appropriate Drive folder.
- [ ] Wait until all docs are converted.
- [ ] Verify conversion: confirm all HTML pages converted to Google Docs.

## After Migration (Immediate Sanity Checks)

- [ ] Spot-check a few docs to ensure:
  - [ ] Titles look reasonable.
  - [ ] Content is present and readable.
  - [ ] Images/tables look sane for a sample.
- [ ] Confirm the number of Google Docs roughly matches the number of pages.

## Optional Follow-Up (Can Be Done Much Later)

- [ ] Apply atomic chunking to selected large docs.
- [ ] Establish naming conventions for new docs.
- [ ] Write a short “How to find things now” note for users.
