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

**Space Consolidation Plan:**

- (Add consolidation plans here)

---

## Phase 2: Space Migration Status

### Migration Status Legend

- ⚪ **Not Started**
- 🟡 **In Progress**
- ✅ **Done**
- ⏭️ **Skipped**
- ➖ **N/A**

### One-Time Setup Steps

1. **Set up Google VM** - One-time setup for all spaces (see [vm-migration-runbook.md](vm-migration-runbook.md))

### Per-Space Migration Steps

1. **Export HTML** - Export Confluence space as HTML
2. **Upload to Drive** - Upload export folder to Google Drive
3. **Convert to Docs** - Enable conversion and verify all pages converted

### Spaces Migration Grid

| Space Key | Space Name               | Export HTML | Upload to Drive | Convert to Docs | Notes                | Export Date | Drive Folder           |
|:----------|:-------------------------|:-----------:|:---------------:|:---------------:|:---------------------|:-----------:|:-----------------------|
| LIV       | Living                   | ✅          | ⚪              | ⚪              | First test migration | 2024-12-03  | Confluence-Living/LIV/ |
| BLOOM     | ALIGN                    | ⚪          | ⚪              | ⚪              |                      |             |                        |
| FIN       | Finances                 | ⚪          | ⚪              | ⚪              |                      |             |                        |
| IC        | Impact Circle            | ⚪          | ⚪              | ⚪              |                      |             |                        |
| LnD       | Learning & Develoopment  | ⚪          | ⚪              | ⚪              |                      |             |                        |
| MOM       | Mom                      | ⚪          | ⚪              | ⚪              |                      |             |                        |
| WE        | Wolf Enterprises         | ⚪          | ⚪              | ⚪              |                      |             |                        |
|           | Michael's Personal Space | ⚪          | ⚪              | ⚪              |                      |             |                        |

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
- Update status by changing ⚪ → 🟡 → ✅
- Add new spaces to the grid as discovered
- Document any issues or special handling in Notes column
- See [pipelines/confluence-pipeline.md](pipelines/confluence-pipeline.md) for detailed step instructions
