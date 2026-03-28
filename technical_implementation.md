# Project Overview
This project addresses a user's critical cloud storage issue. By auditing their data, it was discovered that a note-taking application was consuming a disproportionate amount of space due to its syncing behavior. The solution involved creating a physical backup of all cloud data, strategically removing old and unnecessary files, and educating the user on preventative measures to manage storage effectively. This process successfully reduced their cloud storage utilization from 91% to 48%.

## Milestone 1: Initial Audit & Strategy Formation
**Focus:** Identifying the root cause of high storage consumption and defining a data archival plan.

*   **Investigated the user's storage environment** to understand the scope of the problem.
*   **Confirmed Google Drive was the primary storage consumer** by analyzing their account at one.google.com.
*   **Consulted with the user** to receive approval for a data archival and removal process.
*   **Developed a low-cost strategy:** Export all cloud data to a local, physical hard drive for secure backup and long-term access.

> **Evidence:** See **Initial Storage Analysis**
<img src="Images/Storage%20Before%2091%25.png" alt="A screenshot of Google One storage showing 91% of space used, primarily by Google Drive." width="70%">
<BR>

## Milestone 2: Secure Data Export & Archiving
**Focus:** Creating a complete and verified backup of all Google Drive data to an external drive before any data was deleted from the cloud.

*   **Initiated a full data export** using Google's Takeout service.
*   **Segmented the download into 2 GB chunks** to reduce the risk of file corruption and ensure a reliable backup.
*   **Manually verified the downloaded files** to confirm the data was exported correctly and was fully accessible from the external drive.

> **Evidence:** See **Post-Purge Storage Levels 74%**
<img src="https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/raw/main/Images/Post%20Purge%201.png" alt="A screenshot of Google One storage after the first data purge, showing utilization has dropped to 74%." width="70%">
<BR>

## Milestone 3: First-Pass Data Cleanup (Cold Data)
**Focus:** Removing old, unmodified files (cold data) to reclaim storage space while preserving recent files in the cloud for easy access.

*   **Isolated and removed all files modified before 2024.** This action targeted "cold data" that was no longer actively needed.
*   **Audited the storage again,** which showed a reduction from 91% to 74%.
*   **Conferred with the user, who approved a more aggressive cleanup.** All files from 2024 were also backed up and removed, as they had local copies available.

> **Evidence:** See **Storage Levels After Initial Cleanup**
<img src="https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/raw/main/Images/Post%20Purge%201.png" alt="A screenshot of Google One storage after the first data purge, showing utilization at 74%." width="70%">
<BR>

## Milestone 4: Root Cause Analysis & Targeted Removal
**Focus:** Investigating why initial data purges had a minimal impact and identifying the true source of high storage use.

*   **Identified that the storage reduction to 71% was insufficient,** prompting a deeper investigation.
*   **Used Google Drive's quota tool to sort all files by size.** This revealed that numerous large files with a ".note" extension were the biggest consumers of space.
*   **Traced the files to the "Notability" app** and discovered that its sync process was constantly updating the "last modified" timestamp, which made them invisible to our previous date-based filters.
*   **Confirmed the app's sync was one-way,** meaning the cloud backup could be safely deleted without affecting the original files on the user's tablet.
*   **Disabled the app's auto-sync feature and removed all ".note" files** from the cloud, which immediately freed up a massive amount of space.

> **Evidence:** See **File Analysis Revealing the Root Cause**
<img src="https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/raw/main/Images/Storage%20used%20by%20File%20(Sensitive%20Data%20Redacted).png" alt="A screenshot showing a list of files sorted by size, with .note files taking up the most space." width="70%">
<BR>

## Milestone 5: System Hardening & Client Handoff
**Focus:** Ensuring the user understands the solution and can prevent the issue from recurring.

*   **Confirmed the final storage level dropped to 48%,** an acceptable level for the user.
*   **Verified the user could still access all their critical files,** both from the recent "hot data" left in the cloud and the archived "cold data" on the physical drive.
*   **Educated the user on how to access their physical backups.**
*   **Explained how the Notability app's backup behavior works** and advised on how to manage it going forward to prevent the issue from happening again.

> **Evidence:** See **Final Storage Utilization**
<img src="https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/raw/main/Images/After%20Storage%20Audit.png" alt="A screenshot of the Google One storage page showing the final utilization at 48%." width="70%">
<BR>

## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| Initial date-based file deletions did not significantly reduce storage usage. | The largest files were from a note-taking app (Notability) that constantly updated the "last modified" timestamp every time the app opened. This behavior made the files appear "new," so they were missed by the date-based filters. | Used a different tool (`drive.google.com/drive/quota`) to sort files purely by size. This immediately identified the `.note` files as the problem. After verifying the app's sync behavior, all `.note` files were removed, resolving the storage issue. |
