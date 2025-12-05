# Migration Notes

## VM Approach Abandoned - 2025-12-05

**Decision:** Abandoning Google Cloud VM approach. Easier to drive to a high-speed internet location than deal with cloud fuckery.

**Time wasted:** 7 hours on VM setup, troubleshooting, and fighting with Confluence Cloud export bugs.

**Key Learning:**
- **Cloud is nebulous. Don't go there lightly.**
- It's fuckery all the way down. Vapor built on fluff built on trifle.
- Confluence Cloud export system is broken (stuck tasks, no recovery, no visibility)
- Remote desktop + browser + cloud services = multiple failure points
- Physical location with good internet > cloud VM for this use case

**New approach:** Export directly from local machine with high-speed connection (either at home or drive to location with better bandwidth).

---

## Troubleshooting: Stuck Confluence Export ("Already running this task")

**Problem:** Confluence export shows "Already running this task" error with no progress. The `doexport()` function appears single-threaded, non-reentrant, and can get stuck in a corrupted state.

**IMMEDIATE SOLUTIONS (do these NOW, in order):**

1. **Nuclear option - Clear ALL browser data:**
   - Firefox: Settings → Privacy & Security → Clear Data → Check "Cookies and Site Data" + "Cached Web Content"
   - Or: `Ctrl+Shift+Delete` → Select "Everything" → Clear Now
   - Restart Firefox completely
   - Log back into Confluence and try export again

2. **Try different browser immediately:**
   - Install Chrome on VM: `sudo apt install -y google-chrome-stable`
   - Or use Edge if available
   - Log into Confluence in the new browser
   - Try export from fresh browser session

3. **Try different user account (if you have admin access):**
   - Create a test user or use a different admin account
   - Export from that account - the lock is per-user, not global

4. **Check browser DevTools for stuck requests:**
   - F12 → Network tab
   - Look for any pending requests to `/export` or similar
   - If you see stuck requests, hard refresh (Ctrl+F5) or close all tabs and restart browser

5. **Contact Atlassian Support IMMEDIATELY:**
   - Go to: https://support.atlassian.com/
   - Submit urgent ticket: "Stuck export task blocking migration"
   - Include: Space key, your account, timestamp
   - Request: "Please clear stuck export task for space [SPACE_KEY]"
   - They can reset it server-side in minutes, not hours

6. **Workaround - Export via different method:**
   - Try exporting from a different space first (to verify export works)
   - Then come back to stuck space
   - Or try exporting a subset of pages if possible

**DO NOT:**
- Wait 24 hours (that's bullshit)
- Click Export multiple times (makes it worse)
- Assume it will fix itself

**Root cause:** Confluence Cloud's export system has a per-user lock that can get corrupted. Only browser state reset or Atlassian support can clear it quickly.

---

2025-12-05T16:25:14-05:00

Open Side Bar -> Spaces -> View All Spaces -> RH panel -> SPACE KEY -> ... -> Space Settings

    LH Panel -> General -> Export Space -> Advanced Options -> HTML -> 

    <wolfenterprises.atlassian.net/wiki/spaces/SPACE KEY/settings/export>





SPACE KEY -> ... -> Space settingsmimi



-> Space Settings -> Content -> General ->Export Space
---
2025-12-05T16:10:26-05:00

BLOOM/ALIGN downloaded - 210648
---
2025-12-05T15:59:50-05:00

/wiki/spaces/ALIGN/settings/export
---
2025-12-05T15:14:10-05:00

New IP 34.41.196.208
---
2025-12-05T15:04:44-05:00

https://console.cloud.google.com/compute/instances?project=oval-inquiry-412222
---
2025-12-05T14:53:52-05:00

Created PC in Windows App.  Added IP/password to 1password.
---
2025-12-05T14:14:12-05:00

This ephemeral IP pings from my macBook:

34.10.62.66
---
2025-12-05T14:08:54-05:00

Ran this in ssh

``` bash
sudo apt update
sudo apt install -y ubuntu-desktop xrdp firefox
sudo systemctl enable xrdp
sudo systemctl start xrdp
sudo passwd $USER
```

---
2025-12-05T14:03:57-05:00

Instance created - https://console.cloud.google.com/compute/instancesDetail/zones/us-central1-c/instances/instance-20251205-183322?project=oval-inquiry-412222
---
2025-12-05T13:59:20-05:00

Ready to create VM.
---
2025-12-05T13:57:33-05:00

Installed Remote Desktop, now called (ugh...) Windows App.  How silly is that name?
---
2025-12-05T13:56:20-05:00
IsThird entry
---

2025-12-05T13:54:05-05:00

Second test entry
---

2025-12-05T13:52:35-05:00

Started note log
---

a
AAdd to noteRAdd to notesOn macbook, 