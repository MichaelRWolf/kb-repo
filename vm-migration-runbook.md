# VM Migration Runbook

Confluence → Google Drive/Docs via Cloud VM (Flat Export Default)

This runbook documents a **mechanical, repeatable** workflow for migrating Confluence Cloud spaces to Google Drive, using a Google Cloud VM to avoid slow or unreliable local upload bandwidth.

**Important correction:**  
Confluence **HTML export is always FLAT**.  
It does **not** preserve hierarchy in the filesystem.  
Hierarchy exists *only* in `index.html`, not in folder structure.  
Google Drive cannot reconstruct hierarchy automatically.

This runbook assumes **flat export as the default and only** structure Confluence provides.

---

## 0. Concepts & Naming

- **Confluence site:** `wolfenterprises.atlassian.net`
- **Spaces:** e.g., `LIV`, `BLOOM`, `ALIGN`, etc.
- **Google Drive root for migrated content:**  
  `Confluence-Living/`
- **Per-space target folders:**  
  `Confluence-Living/LIV/`, `Confluence-Living/BLOOM/`, etc.
- **VM name:** `confluence-migrator` (Google Cloud)

Goal: perform *all* large downloads/uploads on the VM.  
Local Mac only handles small files or control tasks.

---

## 1. One-Time Setup: Google Cloud VM

### 1.1 Create a Google Cloud Project

1. Go to: <https://console.cloud.google.com>  
2. Click project selector → **New Project**  
3. Name it: `confluence-migration`  
4. Ensure the new project is active

### 1.2 Enable Compute Engine

1. Left sidebar → **Compute Engine → VM Instances**  
2. If asked, click **Enable API**

### 1.3 Create the VM

1. Click **Create instance**
2. Recommended settings:
   - **Name:** `confluence-migrator`
   - **Machine type:** `e2-medium` (2 vCPU, 4 GB RAM)
   - **Region/Zone:** your choice (any is fine)
3. Boot Disk → **Change**
   - OS: **Ubuntu 22.04 LTS**
   - Size: **20–50 GB**
4. Leave network/firewall defaults
5. Click **Create**

VM boots in ~30 seconds.

---

## 2. One-Time Setup: Desktop & Remote Access

### 2.1 Install Ubuntu Desktop, XRDP, Firefox

1. In VM list: click **SSH** next to `confluence-migrator`
2. Run:

```bash
sudo apt update
sudo apt install -y ubuntu-desktop xrdp firefox
sudo systemctl enable xrdp
sudo systemctl start xrdp
sudo passwd $USER
```

### 2.2 Connect via Remote Desktop (macOS)

1. Install **Microsoft Remote Desktop** from Mac App Store
2. In Google Cloud Console → VM Instances, find External IP  
3. Add New PC in MRD:
   - PC name = External IP  
   - Username = Linux username from SSH prompt  
   - Password = one you set with passwd
4. Connect → You now have a full Ubuntu desktop

---

## 3. One-Time Setup: Shared Google Drive Structure

### 3.1 Create the root shared folder

In Google Drive:

1. Create folder: `Confluence-Living`
2. Right-click → **Share**
3. Add Wendy → **Editor**
4. Click the share settings gear:
   - ✔ Editors can change permissions and share  
   - (Optional) ✔ Allow viewers/commenters to download  

### 3.2 Create per-space placeholders

Inside `Confluence-Living`:

```text
Confluence-Living/
  LIV/
  BLOOM/
  ALIGN/
  ...
```

These inherit the shared permissions.

---

## 4. Per-Space Migration: Confluence → VM

Repeat this section for each space.

### 4.1 Export Confluence Space as HTML (flat)

On the Ubuntu VM (via Remote Desktop):

1. Open **Firefox**
2. Log into Confluence
3. Go to the space (e.g. LIVING)
4. Space settings → **Content Tools → Export**
5. Choose **HTML**
6. Choose **Full Export**
7. Download ZIP (e.g. `Confluence-space-export-Living-194325.html.zip`)

The ZIP goes into `~/Downloads`.

### 4.2 Unzip the export

On the VM terminal:

```bash
cd ~/Downloads
unzip Confluence-space-export-Living-194325.html.zip -d LIV
```

Resulting structure (always flat):

```text
LIV/
  index.html
  <lots of page html files>
  attachments/
  images/
  styles/
```

This is expected and correct.

---

## 5. Per-Space Migration: VM → Google Drive

### 5.1 Prepare destination folder

1. In VM browser → **drive.google.com**
2. Go to `Confluence-Living/LIV/`  
   (create if needed)

### 5.2 Ensure Google Drive converts uploads

Gear icon → Settings:

- ✔ Convert uploaded files to Google Docs editor format

### 5.3 Upload the unzipped folder

1. Inside `Confluence-Living/LIV/`  
2. Click **New → Folder upload**  
3. Select the **LIV/** folder from `~/Downloads`  
4. Confirm

Drive will:

- Upload all `.html`
- Convert each page to a **Google Doc**
- Preserve flat structure (expected)
- Store attachments/images as supporting files

---

## 6. Optional: Flat View Folder with Shortcuts

If you want one folder showing only the Docs:

1. Create: `Confluence-Living/LIV (flat)`
2. Open original `LIV` folder
3. Use search (auto-scoped) → `type:document`
4. Select all results → Right-click → **Add shortcut to Drive**
5. Target = `LIV (flat)`

Nothing moves. Everything is non-destructive.

---

## 7. Cost Control: Stop the VM When Idle

In Google Cloud:

1. Compute Engine → VM Instances  
2. Select `confluence-migrator`  
3. Click **Stop**

Restart as needed.

---

## 8. Optional Next Steps (Not Required for Migration)

- Parse `index.html` to reconstruct original Confluence hierarchy  
- Rename documents to meaningful titles  
- Build AI-first indexing  
- Create reproducible structured Drive layout  
- Automate per-space pipelines

These are enhancements, not part of minimal migration.

---
