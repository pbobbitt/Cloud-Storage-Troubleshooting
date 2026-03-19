# Technical Implementation Log

This document provides a step-by-step technical record of the project phases. It is intended for technical review, auditing, and reproducibility.

---

#### Phase 1: Questioning the User / Storage Audit
The user described an issue of having nearly maxed-out storage. They granted me access to their desktop, and after consulting with them, it was determined they wanted to free cloud space while maintaining access to all data. They believed the issue was simply a high volume of old files but were unsure of the specific makeup or ratio of that data.

The user granted me access to their Windows 11 desktop to troubleshoot. My first step was to open https://one.google.com/ to identify the primary storage consumers. The results indicated that the bulk of the data was held within Google Drive. I spoke with the user, and after a brief consultation, they approved the deletion or archival of data.
* **Observation:** The majority of storage is consumed by Google Drive.
* **Strategic Decision:** Initiated a plan to export cloud data and archive it to a physical drive on the same desktop for a low-cost, effective solution.

> **Evidence:** See [Before Storage Audit](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Before%20Storage%20Audit) in Visual Documentation.

#### Phase 2: Data Export
Began the export of all Google Drive cloud data via https://takeout.google.com/. The data was stored and downloaded on an external hard drive for cold storage backups.
* **Parameters:** Only cloud data for Google Drive was selected for export.
* **Fault Tolerance Strategy:** Segmented the data download into **2 GB** chunks and verified successful downloads by inspecting files to ensure data was properly exported and readable.

#### Phase 3: Data Removal
On Google Drive, I utilized the filter commands `owner:me -is:starred before:2024-03-19` to isolate all files with a "last modified" date before **01/01/2024**. This allowed me to isolate "cold data" for removal. Since the user is a student using multiple devices, I left more recent data available in the cloud to ensure continued access for current classes.
* **Workflow:** Initiated data removal from the SaaS environment only after backups were verified on the external SSD.

#### Phase 4: Storage Audit after Data Removal 1
Re-checked storage usage on Google One to verify the space reclaimed from deleting pre-2024 data. Data usage dropped from **91% to 74%**. While improved, this was not the significant reduction the user requested. I explained to the user that deleting data from before 2024 had reduced utilization to roughly **71%** (reflecting sync delays). They approved the removal of 2024 data as well, as they maintained access to the raw data on their local devices. I reran the filter for data prior to 2025 using the search string: `owner:me before:2025-01-01 -is:starred`.
* **Action:** Verified data removal and contacted the client; however, data utilization remained unacceptably high, prompting further investigation.
* **Technical Justification:** Cloud data is fully backed up in cold storage on an SSD. Cloud storage is intended only for multi-device access, justifying the removal of data not modified since **01/01/2025**.

> **Evidence:** See [Post Purge 1](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Post%20Purge%201) in Visual Documentation.

#### Phase 5: Storage Audit after Data Removal 2
Removing data modified between 2024 and 2025 only decreased storage use by an additional **3%**, leaving utilization at **71%**. This appeared disproportionately high for a data set spanning only 2025 to the present (2026), necessitating a deeper dive.

Since https://one.google.com/ does not allow for sorting files by size, I utilized `drive.google.com/drive/quota` to research the actual storage consumers. I observed that the top results all used the **.note** file extension. Further research identified this as a file type associated with tablet-based note-taking applications. I contacted the client to confirm use of such apps; they identified the app as **Notability**. Upon inspecting the tablet settings, I confirmed the app was syncing all files to Google Drive. Crucially, research indicated that every time the app is opened, it sends an "update pulse" for all documents, refreshing the "last modified" timestamps. This behavior effectively hid these files from my previous date-based filter attempts.

To ensure data integrity, I verified that Notability's cloud sync is a **one-way sync**, meaning files are saved locally on the tablet and cloud backups can be deleted without impacting the primary data. With the user's permission, I disabled the auto-sync feature in Notability and removed all **.note** files from Google Drive (without time restrictions, as they remain stored locally on the tablet).

* **Risk Analysis:** Confirmed Notability settings to ensure cloud backup removal would not result in data loss.
* **Administrative Action:** Purged all **.note** file type data from the cloud environment.
* **Result:** Recovered **30%** storage capacity, lowering data utilization to **48%**.

> **Evidence:**
>
> See [Post Purge 2](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Post%20Purge%202) in Visual Documentation.
>
> See [Storage used by File](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Storage%20used%20by%20File%20(Sensitive%20Data%20Redacted)) in Visual Documentation.
>
> See [Notability Settings](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Notability%20Settings) in Visual Documentation.
>
> See [After Storage Audit](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/After%20Storage%20Audit) in Visual Documentation.

#### Phase 6: System Hardening & Preventive Maintenance
Cloud data utilization dropped to an acceptable level (below **50%**). I verified the user is still able to access all relevant cold data and maintained "hot data" access across multiple devices for recent files.

I educated the user on how to access the physical backups and cautioned them regarding the Notability app's backup behavior, noting that **.note** files consume significant storage.
* **Action:** Client Education and Data Verification completed.

---**Ticket Closed**---

*End of Implementation Log*
