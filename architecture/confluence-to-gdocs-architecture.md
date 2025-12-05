# Confluence → Google Docs Architecture

## Goals

- Input: **Confluence space URL**
- Output: **Google Drive folder** named after the space
- Relationship: **1 Confluence page ⇒ 1 Google Doc** (mechanical, no judgment)
- Zero manual "normalization" during migration.
- No reliance on fragile Google Apps Script for core flow.

## High-Level Flow

```text
Confluence Space
    ↓ (HTML export, bulk)
Space HTML Export (one .html per page)
    ↓ (upload folder to Drive with conversion)
Google Drive Folder (one Google Doc per .html)
    ↓ (optional, later)
Automated post-processing for chunking / AI-indexing
```

## Rationale

- **HTML export** gives:
  - one file per page
  - **flat structure** (no nested folders — hierarchy exists only in `index.html`)
  - titles embedded in `<title>` tags
- **Drive auto-conversion** turns each HTML file into a native Google Doc.
- This provides a **mechanical 1:1 mapping** with no human decisions.
- Hierarchy can be reconstructed from `index.html` if needed (see [hierarchy-reconstruction.md](../hierarchy-reconstruction.md))

## Options for Folder Structure

Since the export is flat, you have two options:

1. **Keep flat structure** (default)
   - Upload the flat export as-is to `/SpaceName/`
   - Pros: simple, search-first, no nesting headaches
   - Cons: loses the sense of hierarchy as a navigation aid

2. **Reconstruct hierarchy** (optional)
   - Parse `index.html` to rebuild the original Confluence tree
   - Upload reconstructed hierarchy to Drive as `<Space Key> (hierarchical)/`
   - Default folder `<Space Key>/` remains flat (no qualifier needed)
   - Can maintain both default (flat) and hierarchical views in parallel
   - See [hierarchy-reconstruction.md](../hierarchy-reconstruction.md) for details
   - Pros: familiar to Confluence users, preserves navigation structure
   - Cons: requires additional processing step

We do **not** hand-edit structure during migration.
Human reorganization can happen later, selectively, if needed.
