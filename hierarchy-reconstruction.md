# Hierarchy Reconstruction Guide
Rebuilding Confluence Structure From Flat HTML Export  
**Supports Parallel “Flat” and “Hierarchical” Views in Google Drive**

Confluence Cloud HTML export is always **flat**.  
Hierarchy exists only inside **`index.html`**, not in folders.

This guide explains how to:

1. Reconstruct the original Confluence hierarchy, **mechanically**.  
2. Upload that reconstructed hierarchy to Drive.  
3. Keep **both** flat and hierarchical versions in parallel:  
   - `Living (Flat)`  
   - `Living (Hierarchical)`  
4. Enable **cross-links** between versions.

---

# 1. What This Produces

After reconstruction and upload, Drive will look like this:

```
Confluence-Living/
  Living (Flat)/              ← All pages, shortcuts or originals
  Living (Hierarchical)/      ← Reconstructed Confluence tree
```

Each contains **the same documents**, just organized differently:

- **Flat:** search-first, AI-friendly, everything in one place  
- **Hierarchical:** human-browseable, legacy Confluence feel  

There is **no duplication of content** unless you explicitly choose it.  
Drive shortcuts can eliminate duplication completely.

---

# 2. Where Reconstruction Happens

Hierarchy reconstruction should be done **on the HTML files before upload**, because:

- The hierarchy is encoded in `index.html`
- HTML filenames map cleanly to pages
- Google Docs move/rename operations are slower and API-dependent

You upload **two different folder structures**:

### A. “Flat” import
Direct upload of the unmodified Confluence export:

```
Confluence-Living/Living (Flat)/
    <all pages as Google Docs>
    attachments/
    images/
```

### B. “Hierarchical” import
Upload a **reconstructed folder tree**:

```
Confluence-Living/Living (Hierarchical)/
    Housing/
        Living-in-real-apartments.html
        Housing-Opportunities.html
    RV/
        RV-Break-in-2024.html
        Leaving-Myrtle-Beach-2022.html
    Taxes/
        ...
```

Google Drive will convert the `.html` pages to Docs automatically inside the folder tree.

---

# 3. How the Reconstruction Works (Overview)

Inputs:
- `index.html` sidebar tree (required)
- exported page HTML files (to extract readable titles)

Outputs:
- `hierarchy-tree.json`
- `rename-map.csv`
- `reconstructed/` folder tree *(for upload as “Living (Hierarchical)”)*

Steps:
1. Parse `index.html` for tree structure  
2. Map titles → filenames  
3. Create folder structure  
4. Move+rename HTML files  
5. Upload to Drive

---

# 4. Creating Both Views in Drive

### Step 1 — Upload flat export (no changes)

On the VM:

```
Confluence-Living/Living (Flat)/
    <upload unzipped HTML folder here>
```

Drive converts `.html` → Google Docs.

Everything stays **flat**.

---

### Step 2 — Reconstruct hierarchy (on VM)

Produce:

```
reconstructed/
  RV/
     Leaving-Myrtle-Beach.html
     RV-Break-in.html
  Housing/
     Living-In-Real-Apartments.html
     Housing-Opportunities.html
```

### Step 3 — Upload reconstructed version

Upload:

```
Confluence-Living/Living (Hierarchical)/
    RV/
    Housing/
    ...
```

Drive will again convert `.html` → Docs, but now placed in the correct folders.

---

# 5. Linking Between Flat & Hierarchical Versions

Because **Google Docs are objects in Drive**, you can do **one of two linking strategies**:

---

## Strategy A — Use Drive Shortcuts (Recommended)
No duplication of files.  
Each view is just a different arrangement of pointers.

### Implementing A:
1. Upload the **Hierarchical** version (converted to Google Docs)
2. Upload the **Flat** version using **shortcuts**:
   - Search for all Google Docs inside `Living (Hierarchical)`
   - Select all → Right-click → **Add shortcut to Drive**
   - Choose: `Living (Flat)`

Result:

- **Hierarchical** holds the *real files*
- **Flat** holds *shortcuts* to the same files

### Benefits
- Single source of truth  
- Both layouts always stay in sync  
- No duplicate storage  
- Links and permissions are unified  

---

## Strategy B — Duplicate the Docs (Not recommended)
Drive allows duplication, but:

- Uses more storage  
- Creates two independent docs  
- They drift  
- Links do not stay synchronized  

Only use this if you explicitly want “archival snapshots."

---

# 6. Links Between Views

If using **shortcuts** (Strategy A):

### Linking from “Flat” → “Hierarchical”
Shortcuts already point directly to real files inside `Living (Hierarchical)`.  
Clicking a shortcut opens the canonical location automatically.

### Linking from “Hierarchical” → “Flat”
You can insert links in several ways:
- Right-click the file → “Copy link” → paste link into a Doc  
- Insert → Link → paste Drive link  
- Doc-to-Doc links remain stable even if you rename folders

Because both views point to the **same file objects**, links never break.

---

# 7. Which Version Should Hold the “Real” Files?

### Choose one:
1. **Hierarchy as real content**  
   Flat is shortcuts  
   (recommended if migrating from Confluence mindset)

2. **Flat as real content**  
   Hierarchy is shortcuts  
   (recommended if AI-first and structure is secondary)

### Default Recommendation:
**Hierarchy = real  
Flat = shortcuts**

Because:
- Confluence was hierarchy-first  
- Drive search works equally well across both  
- AI tools don’t care which folder holds the actual files

---

# 8. Summary of Parallel Views

You will end up with:

```
Confluence-Living/
  Living (Hierarchical)/   ← REAL FILES
      RV/
      Housing/
      ...
  Living (Flat)/           ← SHORTCUT VIEW
      <shortcuts to all docs>
```

This arrangement is:

- fully consistent  
- low maintenance  
- reversible  
- intuitive for humans  
- AI-friendly  

---

# 9. Adding New Files to Both Views

When you create a new document, follow this workflow to keep both views synchronized:

## Workflow for New Files

### Step 1 — Create the file in the hierarchical structure

1. Navigate to the appropriate folder in `Living (Hierarchical)/`
   - Example: Create "New-RV-Project" in `Living (Hierarchical)/RV/`
2. Create the new Google Doc in that location
   - This becomes the **canonical location** (real file)

### Step 2 — Add shortcut to flat view

1. Right-click the new file in `Living (Hierarchical)/`
2. Select **Add shortcut to Drive**
3. Choose destination: `Living (Flat)/`
4. Click **Add shortcut**

Result: The new file is now visible in both views:

- **Hierarchical:** Real file in its category folder
- **Flat:** Shortcut pointing to the same file

## Best Practices

### Where to create new files

- **Always create in `Living (Hierarchical)/`** (the real files location)
- Choose the appropriate subfolder based on topic/category
- If unsure, create in the root of `Living (Hierarchical)/` and organize later

### Maintaining both views

- **New files:** Create in hierarchical → add shortcut to flat
- **Moving files:** Move the real file in hierarchical → shortcut in flat updates automatically
- **Renaming files:** Rename the real file in hierarchical → shortcut in flat reflects the new name
- **Deleting files:** Delete from hierarchical → shortcut in flat becomes broken (delete it too)

### Automation option

For frequent additions, consider:

- A simple script or workflow that:
  1. Detects new files in `Living (Hierarchical)/`
  2. Automatically creates shortcuts in `Living (Flat)/`
- Or a periodic manual sync: select all new files → bulk add shortcuts

## Why This Works

Because shortcuts point to the **same file object**:

- Edits appear in both views immediately
- Permissions are unified
- No sync issues or drift
- Single source of truth maintained

---

# 10. Next Steps

If you provide:

- `index.html`
- list of exported `.html` files

I can generate:

- the hierarchy tree  
- rename map  
- folder layout  
- fully reconstructed structure folder  
- instructions or script to create shortcuts for the flat view  
