# Confluence Export Tooling

We intentionally keep the core migration path **simple** and rely on:

- Confluence's built-in **HTML export** per space.
- Google Drive's built-in **HTML → Google Docs** conversion.

## Required Tooling

- Access to Confluence with permission to export spaces.
- Access to a Google Workspace / Drive account with enough storage.
- A browser or basic CLI tools for:
  - downloading export archives
  - unzipping them
  - uploading folders to Drive

## Optional Tooling (Nice-to-Haves)

These are not required but may help:

- Small scripts to:
  - validate export completeness (page counts)
  - rename or move folders in bulk after upload
- Future automation to:
  - perform atomic chunking via APIs
  - build an index of exported pages vs migrated docs

The baseline is deliberately low-complexity so that the migration does not depend on
fragile or one-off automation.
