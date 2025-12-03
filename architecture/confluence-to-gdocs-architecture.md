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
  - folder structure that mirrors the space
  - titles embedded in `<title>` tags
- **Drive auto-conversion** turns each HTML file into a native Google Doc.
- This provides a **mechanical 1:1 mapping** with no human decisions.

## Options for Folder Structure

Two mechanical options, chosen once per migration:

1. **Preserve Confluence-like tree**  
   - Keep the export’s nested folders when uploading to Drive.  
   - Pros: familiar to Confluence users.  
   - Cons: deep trees can still be brittle; search will eventually dominate.

2. **Flatten to a single folder**  
   - Upload everything into `/SpaceName/`.  
   - Pros: simple, search-first, no nesting headaches.  
   - Cons: loses the sense of hierarchy as a navigation aid.

We do **not** hand-edit structure during migration.
Human reorganization can happen later, selectively, if needed.
