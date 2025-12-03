# Confluence → Google Docs Pipeline (Mechanical)

This is the **mechanical, no-brainpower** pipeline.

## Step 1 — Export Confluence Space as HTML

From Confluence:

- Export the entire space as **HTML** (not PDF, not single Word).
- **Important:** Confluence HTML export is **always flat** — no nested folders.
- Hierarchy exists only in `index.html`, not in the filesystem structure.
- Result: a directory like:

```text
space-key-export/
    index.html
    page-1.html
    page-2.html
    page-3.html
    attachments/
    images/
    styles/
    ...
```

## Step 2 — Upload Export Folder to Google Drive

In Google Drive:

1. Create a folder named after the space, e.g. `SpaceName`.
2. Upload the entire export folder.
3. Enable “Convert uploaded files to Google Docs format”.

Result:

- Each `*.html` page becomes a **Google Doc**.
- Filenames are derived from page titles (from the HTML `<title>` tag).

No merging, splitting, or renaming decisions needed here.

## Step 3 — Choose Folder Strategy (Once)

Since the export is flat, you have two options:

1. **Keep flat structure** (default)
   - Upload the flat export as-is to `/SpaceName/`
   - All pages in one folder, search-first approach

2. **Reconstruct hierarchy** (optional, see [hierarchy-reconstruction.md](../hierarchy-reconstruction.md))
   - Parse `index.html` to rebuild the original Confluence tree
   - Upload reconstructed hierarchy to Drive
   - Can maintain both flat and hierarchical views in parallel

This is a bulk operation; no per-page thinking.

## Step 4 — Optional Post-Processing (Later, Not Required Today)

After migration, we *may*:

- auto-chunk large docs into smaller "section docs"
- auto-generate an index doc
- auto-tag or classify docs for future AI retrieval

These are described in more detail in:

- [gdocs-atomic-chunking-pipeline.md](pipelines/gdocs-atomic-chunking-pipeline.md)
- [auto-chunking-algorithm.md](automation/auto-chunking-algorithm.md)
- [auto-indexing-ai.md](automation/auto-indexing-ai.md)

They are **optional** and not part of the minimum viable migration.
