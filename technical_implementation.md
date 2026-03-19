# Technical Implementation Log

This document provides a step-by-step technical record of the project phases. It is intended for technical review, auditing, and reproducibility.

---

#### Phase 1: Questioning the User / Storage Audit
User described their issue of having nearly maxxed out storage they gave me access to their desktop and after talking with them they were just wanted to free cloud space but still wanted to keep access to any data. they think that they just had alot of old files but had no idea what the make up or ratio of that data may have been.

user granted me access to their windows 11 desktop to troubleshoot. my first step was to open https://one.google.com/ to see what was taking up the most space. once viewing the result it turned out that the bulk of data was from google drive. I spoke with the user, and after a bit of back and forth, they were ok with deleting or archiving data. 
* **Observation:** Most of the data is taken by google drive
* **Strategic Decision:** seems like a simple fix just need to export this data and archive to a physical drive on the same desktop.

> **Evidence:** See [Before Storage Audit](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Before%20Storage%20Audit) in Visual Documentation.

#### Phase 2: Data Export
Began the export of all Google Drive cloud data via https://takeout.google.com/ , stored downloaded on external hardrive for cold storage backups 
* **Parameters:** only cloud data for google drive was removed
* **Fault Tolerance Strategy:** Segmented download of data to 2 GB chunks and verified successful download by inspecting files to ensure data was properly exported.


#### Phase 3: Data removal
On Google drive i used the filter commands owner:me -is:starred before:2024-03-19 to isolate all files that have the last modified date of before 1/1/2024 to isolate cold data that can be removed, since the user is a student who uses multiple devices left more recent data available on the cloud so they could still access any data they may need for current classes.
* **Workflow:** Initiated the data removal from Saas enviroment after backups were verified on SSD

#### Phase 4: Storage Audit after Data Removal 1
Checked used storage usage on google one again to see how much space was freed from deleting data pre 2025. data usage dropped from 91% to 74% this was ok but not the big reduction the user was looking for. so i reached back out to the user explain deleting data from before 2024 had reduced data to 71% they advised they were ok to also remove data from 2024 as they still had access to the raw data this was just back up on the could for multi device use. so i reran the filter but this time for data from 2025 used search filter "owner:me before:2025-1-1 -is:starred"
* **Action:** verified data was removed, contacted client but data utilaztion was still too high so initated removal of more data.
* **Technical Justification:** The cloud data removed is backed up in cold storage with a SSD, this cloud is just for the user to have access with multiple device so data was removed that had not been modified since jan 1/1 2025

>**Evidence:** See [Post Purge 1](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Post%20Purge%201) in Visual Documentation.

#### Phase 5: Storage Audit after Data Removal 2
Removinng data last modified from 2024 - 2025 only decreased storage use by 3% this left utlization still at 71% which seemed very high for data only from 2025 - present 2026 so i did a deeper dive.

using https://one.google.com/ doesnt allow to sort files by size so i used drive.google.com/drive/quota to research what was actually using all the space. once i looked there i realized the top results all ended in .note i was unfimiliar but after reseacheing it was discovered this was a file type associated with note taking apps on tablets. i reached back out to the client to see if they used a note taking app on any other devices out side of the desktop they wanted to troubleshoot the said they used a note taking app called Notability which allows them to hand write notes on their tablet. i gained access to the tablet to inspect and when looking at the settings it showed the the app was sysncing all of its files to google drive. importantly after more research i found out every time this app is opened it sends a update pulse for all documents so every note the user had on this had "last modified" time stamps updated which is why files that were older then the previous searches were hidden from my filter attempts. 

to ensure data was not lost i verified that Notability's cloud sync was a one way sync so files are actually saved locally and the cloud can be deleted with no issues. so with the users permission we disabled the auto sync for this Notability app and then removed all files from google drive with the file type .note (no time limit rescrtion as they are all saved locally to the tablet)

* **Risk analysis:** Confirmed Notablity settings before removing cloud backup do prevent data loss.
* **Administrative Action:** Purged .note file type data.
* **Result:** Recovered 30% storage capacity lowering data utilization down to 49% 

>**Evidence:**
>
>See [Post Purge 2](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Post%20Purge%202) in Visual Documentation.
>
>See [Storage used by File](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/%09%20Storage%20used%20by%20File%20(Sensitive%20Data%20Redacted)) in Visual Documentation.
>
>See [Notability Settings](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Notability%20Settings) in Visual Documentation.
>
>See [After Storage Audit](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/After%20Storage%20Audit) in Visual Documentation.

#### Phase 6: System Hardening & Preventative Maintenance
Cloud Data utilization dropped to acceptible levels of below 50%, verified user is still able to access all relevant cold data, (they were happy i was able to maintain recent hot data access across multiple devices)

educated user on how to acess the back ups and warned about the Notablity app backing up to the cloud as .note files hog a lot of storage. 
* **Action:** Client Education and Data Verification

---**Ticket Closed**--

*End of Implementation Log*
