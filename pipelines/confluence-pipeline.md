# Confluence → Google Docs Pipeline (Mechanical)

This is the **mechanical, no-brainpower** pipeline for migrating each Confluence space.

**Note:** One-time setup (Google VM) is documented in [vm-migration-runbook.md](../vm-migration-runbook.md).

## Per-Space Migration Steps

### Step 1 — Export Confluence Space as HTML

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

### Step 2 — Upload Export Folder to Google Drive

In Google Drive:

1. Create a folder named after the space, e.g. `SpaceName`.
2. Enable "Convert uploaded files to Google Docs format" (in Drive settings).
3. Upload the entire export folder to the destination folder.
4. Wait for conversion to complete (Drive converts `.html` files to Google Docs automatically).

Result:

- Each `*.html` page becomes a **Google Doc**.
- Filenames are derived from page titles (from the HTML `<title>` tag).
- All pages are in a flat structure (default).

No merging, splitting, or renaming decisions needed here.

### Step 3 — Verify Conversion

- Confirm all HTML pages have been converted to Google Docs.
- Spot-check a few documents to ensure content is readable.
- Verify the number of Google Docs matches the number of pages.

### Step 4 — Optional: Reconstruct Hierarchy

Since the export is flat, you can optionally reconstruct the original Confluence hierarchy:

- Parse `index.html` to rebuild the original Confluence tree
- Upload reconstructed hierarchy to Drive
- Can maintain both flat and hierarchical views in parallel
- See [hierarchy-reconstruction.md](../hierarchy-reconstruction.md) for detailed instructions

**Default:** Keep flat structure (already done in Step 2). All pages in one folder, search-first approach.

This is a bulk operation; no per-page thinking.

---

## Optional: Post-Processing (Later, Not Required Today)

After migration, we *may*:

- auto-chunk large docs into smaller "section docs"
- auto-generate an index doc
- auto-tag or classify docs for future AI retrieval

These are described in more detail in:

- [gdocs-atomic-chunking-pipeline.md](pipelines/gdocs-atomic-chunking-pipeline.md)
- [auto-chunking-algorithm.md](automation/auto-chunking-algorithm.md)
- [auto-indexing-ai.md](automation/auto-indexing-ai.md)

They are **optional** and not part of the minimum viable migration.
