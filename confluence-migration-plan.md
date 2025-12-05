# Confluence Migration Plan

**Account:** wolfenterprises.atlassian.net  
**Last Updated:** 2024-12-03

---

## Phase 1: Space Cleanup & Consolidation

### 1.1 Prune Dead Spaces

- [ ] Audit all spaces for activity
- [ ] Identify spaces with no recent updates (threshold: TBD)
- [ ] Archive or delete dead spaces
- [ ] Document pruned spaces and rationale

**Dead Spaces Identified:**

- (Add spaces here as identified)

### 1.2 Combine Related Spaces

- [ ] Identify related/overlapping spaces
- [ ] Plan consolidation strategy
- [ ] Execute space merges
- [ ] Verify merged content integrity

**Space Consolidation Options:**

#### Option A: Merge in Confluence (Not Recommended)

- Confluence does not support merging entire spaces
- Can move pages manually (Space Tools → Content Tools → Move)
- Limitations: breaks links, loses metadata, very time-consuming
- Not practical for large consolidations

#### Option B: Merge After Migration to Google Drive (Recommended) **SELECTED**

- Export both spaces separately as HTML
- Upload both to Google Drive (convert to Docs)
- Merge folders in Drive after conversion
- Preserves all content, easier than Confluence moves
- Can reorganize structure in Drive without breaking links
- **Post-processing step:** After migration, merge space folders in Drive and update "Merged to" column in migration grid

**Space Consolidation Plan:**

- (Add consolidation plans here)

---

## Phase 2: Space Migration Status

### Migration Status Legend

| Indicator | Description           |
|:----------|:----------------------|
| ____      | Not yet begun         |
| WIP       | Work In Progress      |
| DONE      | Completed             |
| -->       | Intentionally skipped |
| N/A       | Not Applicable        |

### One-Time Setup Steps

1. **Set up Google VM** - One-time setup for all spaces (see [vm-migration-runbook.md](vm-migration-runbook.md))

### Per-Space Migration Steps

1. **Export HTML** - Export Confluence space as HTML (always flat — hierarchy in `index.html` only)
2. **Upload to Drive** - Upload export folder to Google Drive with conversion enabled
   - Create destination folder in Drive
   - Enable "Convert uploaded files to Google Docs format" (in Drive settings)
   - Upload the entire export folder to the destination folder
   - Wait for conversion to complete (Drive converts `.html` files to Google Docs automatically)
3. **Verify Conversion** - Confirm all pages converted to Google Docs
   - Confirm all HTML pages have been converted to Google Docs
   - Spot-check a few documents to ensure content is readable
   - Verify the number of Google Docs matches the number of pages
4. **Optional: Reconstruct Hierarchy** - Parse `index.html` to rebuild tree structure (see [hierarchy-reconstruction.md](hierarchy-reconstruction.md))
5. **Post-Processing: Merged to** - If this space was merged into another space in Drive, record the parent space key (e.g., "LIV") or "N/A" if not merged

### Spaces Migration Grid

| Space Key | Space Name               | Export HTML | Upload to Drive | Verify Conversion | Merged to | Notes                |
|:----------|:-------------------------|:------------|:----------------|:------------------|:----------|:---------------------|
| LIV       | Living                   | DONE        | ____            | ____              | N/A       | First test migration |
| BLOOM     | ALIGN                    | ____        | ____            | ____              | N/A       |                      |
| FIN       | Finances                 | ____        | ____            | ____              | N/A       |                      |
| IC        | Impact Circle            | ____        | ____            | ____              | N/A       |                      |
| LnD       | Learning & Develoopment  | ____        | ____            | ____              | N/A       |                      |
| MOM       | Mom                      | ____        | ____            | ____              | N/A       |                      |
| WE        | Wolf Enterprises         | ____        | ____            | ____              | N/A       |                      |
|           | Michael's Personal Space | ____        | ____            | ____              | N/A       |                      |

### SPACES to Consolidate

Spaces found but not yet in migration grid (evaluate for consolidation or separate migration):

- **BLOOM Projects** - Consider consolidating with BLOOM
- **Coaching**
- **Fidelity Investment & Eliassen Group**
- **Hillrom**
- **Radtac**
- **Software Engineer Program**
- **Soul Leadership**

---

## Phase 3: Post-Migration Tasks

### Per-Space Post-Migration

- [ ] Verify document count matches page count
- [ ] Spot-check content quality
- [ ] Verify images/attachments preserved
- [ ] Test search functionality
- [ ] Create "How to find things" guide for users

### Global Post-Migration

- [ ] Build index of all migrated spaces
- [ ] Establish naming conventions
- [ ] Set up AI-first indexing (optional)
- [ ] Document migration lessons learned

---

## Notes

- **Set up Google VM** is a one-time task (done once, applies to all spaces)
- Update status by changing "Not Started" → "WIP" → "DONE"
- Add new spaces to the grid as discovered
- Document any issues or special handling in Notes column
- See [pipelines/confluence-pipeline.md](pipelines/confluence-pipeline.md) for detailed step instructions
