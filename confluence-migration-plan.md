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

Confluence Export URLs

| Space Key                | Space Name                           | Confluence Export URL                                                      | Status |
|--------------------------|--------------------------------------|----------------------------------------------------------------------------|--------|
| LIV                      | Living                               | https://wolfenterprises.atlassian.net/wiki/spaces/LIV/settings/export      | Done   |
| ALIGN                    | BLOOM                                | https://wolfenterprises.atlassian.net/wiki/spaces/ALIGN/settings/export    | Done   |
| FIN                      | Finances                             | https://wolfenterprises.atlassian.net/wiki/spaces/FIN/settings/export      | 232356 |
| IC                       | Impact Circle                        | https://wolfenterprises.atlassian.net/wiki/spaces/IC/settings/export       | WIP    |
| LnD                      | Learning & Develoopment              | https://wolfenterprises.atlassian.net/wiki/spaces/LnD/settings/export      |        |
| MOM                      | Mom                                  | https://wolfenterprises.atlassian.net/wiki/spaces/MOM/settings/export      |        |
| WE                       | Wolf Enterprises                     | https://wolfenterprises.atlassian.net/wiki/spaces/WE/settings/export       |        |
|--------------------------|--------------------------------------|----------------------------------------------------------------------------|--------|
| Michael's Personal Space | ____                                 | ____                                                                       |        |
|--------------------------|--------------------------------------|----------------------------------------------------------------------------|--------|
| Projects                 | BLOOM Projects                       | https://wolfenterprises.atlassian.net/wiki/spaces/Projects/settings/export |        |
| COAC                     | Coaching                             | https://wolfenterprises.atlassian.net/wiki/spaces/COAC/settings/export     |        |
| FIEG                     | Fidelity Investment & Eliassen Group | https://wolfenterprises.atlassian.net/wiki/spaces/FIEG/settings/export     |        |
| HR                       | Hillrom                              | https://wolfenterprises.atlassian.net/wiki/spaces/HR/settings/export       |        |
| RAD                      | Radtac                               | https://wolfenterprises.atlassian.net/wiki/spaces/RAD/settings/export      |        |
| SEP                      | Software Engineer Program            | https://wolfenterprises.atlassian.net/wiki/spaces/SEP/settings/export      |        |
| DLC                      | Soul Leadership                      | https://wolfenterprises.atlassian.net/wiki/spaces/DLC/settings/export      |        |
|--------------------------|--------------------------------------|----------------------------------------------------------------------------|--------|

Google Drive Imported URLs

| Space Key                | Space Name                           | Google Drive URL                                                         |
|--------------------------|--------------------------------------|--------------------------------------------------------------------------|
| LIV                      | Living                               | https://drive.google.com/drive/folders/1mqqPMoQee0mCwGiis9FQl5CpGaKZEuLH |
| ALIGN                    | BLOOM                                | https://drive.google.com/drive/folders/1z8V-hVyvt9zTqrLauRgFd9B_W2CSVxqR |
| FIN                      | Finances                             | https://drive.google.com/drive/folders/1ftip4KjBndhD1NksKfCT8xp7vSYF_99A |
| IC                       | Impact Circle                        |                                                                          |
| LnD                      | Learning & Develoopment              |                                                                          |
| MOM                      | Mom                                  |                                                                          |
| WE                       | Wolf Enterprises                     |                                                                          |
|--------------------------|--------------------------------------|--------------------------------------------------------------------------|
| Michael's Personal Space | ____                                 |                                                                          |
|--------------------------|--------------------------------------|--------------------------------------------------------------------------|
| Projects                 | BLOOM Projects                       |                                                                          |
| COAC                     | Coaching                             |                                                                          |
| FIEG                     | Fidelity Investment & Eliassen Group |                                                                          |
| HR                       | Hillrom                              |                                                                          |
| RAD                      | Radtac                               |                                                                          |
| SEP                      | Software Engineer Program            |                                                                          |
| DLC                      | Soul Leadership                      |                                                                          |
|--------------------------|--------------------------------------|--------------------------------------------------------------------------|
On



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
