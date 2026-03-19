# SaaS Storage Optimization & Data Lifecycle Management

## Executive Summary
This project addressed a critical storage exhaustion event (91% capacity) within a Google Workspace environment that threatened service continuity for Gmail and Drive. By performing Root Cause Analysis (RCA) on third-party application sync behavior, I recovered 43% of system capacity and implemented a sustainable archival strategy.

* **Primary Skill:** SaaS Administration & Storage Troubleshooting
* **Certification Alignment:** CompTIA A+, Cloud+

## The Scenario
The user's primary cloud storage reached a 91% critical threshold, creating an immediate risk of service interruption for incoming emails and document synchronization. As the user is an active student, the requirement was to maintain "Hot" access to current course materials while identifying and archiving "Cold" legacy data to free up primary cloud resources.

## Environment & Tools
* **Platform/OS:** Google Workspace (Cloud), iPadOS (Local), Windows 11 (Archive Host)
* **Tools Used:** Google Drive, Google One, Google Takeout, Notability, NTFS External Storage
* **Methodology:** CompTIA 6-Step Troubleshooting Theory, Data Lifecycle Management (DLM)

## Deployment & Execution

### 1. Requirements & Scope
* **Goal:** Reduce cloud storage utilization to the "Green Zone" (sub-50%) while preserving user access to active academic materials.
* **Constraint:** No Budget / Zero-Cost. The solution must utilize existing hardware (External NTFS Drive) and free tiers of existing SaaS tools.
* **Scope:** 15 GB Google Workspace account; identifying and migrating approximately 6.5 GB of stale data.

### 2. Design & Strategy
* **Immediate Action (The "Fix"):** Perform a comprehensive storage audit using Google One to identify the primary "storage hogs." The strategy focused on moving "Cold Data" (archived files) from the cloud to local physical storage, ensuring the user retains access while immediately dropping below the critical 91% threshold.
* **Strategic Shift (The "Future-Proof"):** During the audit, it was discovered that a note-taking application (Notability) was auto-syncing `.note` files to the cloud, consuming excessive space. Because the "Live" data was already stored locally on the iPad and synced via iCloud, these cloud backups were redundant. To prevent future storage exhaustion, the strategy shifted to disabling the redundant auto-backup and archiving the legacy 2022/2023 academic data to an external NTFS drive.

### 3. Implementation Summary
The project was executed through a methodical 7-phase workflow. For the granular technical procedures and configuration steps associated with each phase, refer to the **[Full Implementation Log](technical_implementation.md)**.

| Phase | Milestone | Key Technical Action |
| :--- | :--- | :--- |
| **Phase 1** | Audit & Discovery | Utilized Google One and Drive Quota tools to identify Google Drive as the primary storage consumer. |
| **Phase 2** | Design & Planning | Initiated Google Takeout for full account export to establish a "fail-safe" backup before deletion. |
| **Phase 3** | Deployment/Execution | Executed targeted search filters (`before:2024-03-19`) to isolate legacy cold data. |
| **Phase 4** | Migration/Integration | Migrated 2022–2024 archives to local NTFS storage in 2GB segmented chunks. |
| **Phase 5** | QA & Verification | Performed a secondary audit; identified `.note` files as the remaining high-utilization culprit. |
| **Phase 6** | Policy Hardening | Disabled Notability Auto-Sync after verifying 1-way sync logic to prevent future bloat. |
| **Phase 7** | Final Documentation | Verified sub-50% utilization and educated user on local backup access. |

### 4. Quality Assurance (QA) & Verification

**Technical Validation (The Proof)**
* **Tool Used:** Google Drive Quota Tool & Local File Explorer.
* **Logic:** By comparing the cloud quota before and after the manual purge of `.note` files, I verified a 30% instantaneous reduction in used capacity.

| Test Case | Expected Result | Actual Result | Status |
| :--- | :--- | :--- | :--- |
| **Integrity Check** | Exported ZIP files open and contain readable files. | Verified via manual inspection of E: Drive. | **Verified** |
| **Cloud Recovery** | Total storage drops below 7.5 GB (50%). | Final storage confirmed at 48% (7.2 GB). | **Verified** |
| **Sync Safety** | Deleting cloud `.note` files leaves iPad files intact. | Verified via Notability 1-way sync documentation. | **Verified** |

**Functional & Architectural Validation**
* **User Experience:** User confirmed incoming emails are no longer blocked and 2026 course materials remain synced.
* **Storage Tiering:** Established a clear boundary between "Hot" (Cloud/Recent) and "Cold" (Local/Archive) data.

### 5. Documentation & Maintenance
* **Standard Operating Procedure (SOP):** Perform a manual Google Takeout export at the end of every academic semester.
* **Audit Schedule:** Review Google Drive Quota once every 90 days to check for "Shadow Syncing" from new applications.
* **Redundancy (3-2-1 Compliance):** Academic data now exists on the iPad (Active), External SSD (Backup 1), and Google Takeout Archives (Backup 2).

## Troubleshooting Log

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| **Metadata Mismatch** | Date-based filters failed to find old files. | Discovered Notability "Update Pulse" refreshed "Last Modified" dates daily. Resolved by searching via file extension (`.note`). |
| **Quota Latency** | Storage bar didn't drop immediately after delete. | Identified Google Drive "Trash" still holding objects. Performed "Empty Trash" to force quota update. |

## Key Achievements & Insights
* **Risk Mitigation:** Prevented an imminent "Mail Block" that would have disrupted critical academic communications.
* **Infrastructure Redesign:** Transitioned from a "Cloud-Only" unstructured model to a Hybrid Tiered Storage model.
* **Data Integrity:** Ensured 100% data retention by using segmented exports and local verification before cloud-side purging.
* **Efficiency/ROI:** Reclaimed ~7GB of space (avoiding subscription upgrades) using existing local hardware.

## Technical Competencies Demonstrated
* **SaaS Administration:** Expert-level navigation of Google Workspace admin and quota tools.
* **Data Lifecycle Management (DLM):** Applying the logic of archiving "Cold" data to save costs on "Hot" storage resources.
* **Root Cause Analysis (RCA):** Identifying that application-specific sync behavior—not just file volume—was the driver of storage bloat.

## Visual Documentation

**Initial State / Evidence** <img src="Images/Before Storage Audit.png" alt="91% Storage Utilization" width="70%">

**Post-Configuration / Verification** <img src="Images/After Storage Audit.png" alt="48% Storage Utilization" width="70%">

## Disclaimer & AI Disclosure
While the **technical architecture, troubleshooting, data migration, and verification** of this lab were performed entirely by the author, **Generative AI** was utilized as a collaborative tool to assist in structured formatting, professional terminology refinement, and documentation of this report.
