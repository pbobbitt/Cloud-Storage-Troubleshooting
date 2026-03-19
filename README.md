# SaaS Storage Optimization & Data Lifecycle Management

## Executive Summary
This project addressed a critical storage exhaustion event (91% capacity) within a Google Workspace environment that threatened service continuity for Gmail and Drive. By performing Root Cause Analysis (RCA) on third-party application sync behavior, I recovered 43% of system capacity and implemented a sustainable archival strategy.

* **Primary Skill:** SaaS Administration & Storage Troubleshooting
* **Certification Alignment:** CompTIA A+, Cloud+

## The Scenario
The User's primary cloud storage reached a 91% Critical threshold, creating an immediate risk of service interruption for incoming emails and document synchronization. The user is a student, so they wanted to keep recent files, but were ok with older files being deleted/archived to free space.

## Environment & Tools
* **Platform/OS:** Google Workspace (Cloud), iPadOS (Local), Windows 11 (Archive Host)
* **Tools Used:** Google Drive, Google one, Google takeout, Notability, NTFS External Storage
* **Methodology:** CompTIA 6-Step Troubleshooting Theory, Data Lifecycle Management (DLM)

## Deployment & Execution

### 1. Requirements & Scope
* **Goal:** Reduce cloud storage utilization to the "Green Zone" (sub-50%) while preserving user access to active academic materials.
* **Constraint:** No Budget / Zero-Cost. The solution must utilize existing hardware (External NTFS Drive) and free tiers of existing SaaS tools.
* **Scope:** 15 GB Google Workspace account; identifying and migrating approximately 6.5 GB of stale data.

### 2. Design & Strategy
[Explain the logic behind your approach before execution.]

* **Immediate Action (The "Fix"):** Perform a comprehensive storage audit using Google One to identify the primary "storage hogs." The strategy was to move "Cold Data" (archived files) from the cloud to local physical storage, ensuring the user retains access while immediately dropping below the critical 91% threshold.
* **Strategic Shift (The "Future-Proof"):** During the audit, it was discovered that the user had a note-taking application (Notability) on their iPad that was auto-syncing .note files to the cloud, which took an excessive amount of space. Because the "Live" data was already stored locally on the iPad, these cloud backups were redundant. To prevent future storage exhaustion, the strategy shifted to disabling the redundant auto-backup on the Notability app and archiving the legacy 2022/2023 academic data from the cloud to an external NTFS drive.

### 3. Implementation Summary
The project was executed through a methodical 7-phase workflow. For the granular technical procedures, specific CLI commands, and configuration steps associated with each phase, refer to the **[Full Implementation Log](technical_implementation.md)**.

| Phase | Milestone | Key Technical Action |
| :--- | :--- | :--- |
| **Phase 1** | Audit & Discovery | [Action taken] |
| **Phase 2** | Design & Planning | [Action taken] |
| **Phase 3** | Deployment/Execution | [Action taken] |
| **Phase 4** | Migration/Integration | [Action taken] |
| **Phase 5** | QA & Verification | [Action taken] |
| **Phase 6** | Policy Hardening | [Action taken] |
| **Phase 7** | Final Documentation | [Action taken] |

### 4. Quality Assurance (QA) & Verification

**Technical Validation (The Proof)**
* **Tool Used:** [e.g., PowerShell Get-FileHash, Ping, Wireshark]
* **Logic:** [e.g., "By generating a unique digital fingerprint (hash), I can verify data matches the source."]

| Test Case | Expected Result | Actual Result | Status |
| :--- | :--- | :--- | :--- |
| [Test 1] | [What should happen] | [What did happen] | **Verified** |
| [Test 2] | [What should happen] | [What did happen] | **Verified** |

**Functional & Architectural Validation**
* [Point 1: User-end experience check]
* [Point 2: System-level check/IAM verification]

### 5. Documentation & Maintenance
[Proactive steps for long-term health.]

* **Standard Operating Procedure (SOP):** [Recurring task description]
* **Audit Schedule:** [How often do you check for system drift?]
* **Redundancy (3-2-1 Compliance):** [Backup or air-gapping strategy]

## Troubleshooting Log
[Documents your ability to solve unforeseen technical hurdles.]

| Issue Encountered | Root Cause Analysis | Resolution & Verification |
| :--- | :--- | :--- |
| [The Error] | [Why it happened] | [How you fixed it] |

## Key Achievements & Insights
* **Risk Mitigation:** [What disaster or lockout did you prevent?]
* **Infrastructure Redesign:** [How is the architecture more resilient now?]
* **Data Integrity:** [How did you ensure 100% accuracy?]
* **Efficiency/ROI:** [Did you save time, money, or storage?]

## Technical Competencies Demonstrated
* **[Competency 1]:** [Detailed explanation of how you used this skill]
* **[Competency 2]:** [Detailed explanation of how you used this skill]

## Visual Documentation

**Initial State / Evidence**
<img src="images/before.png" alt="Description of initial state" width="70%">

**Post-Configuration / Verification**
<img src="images/after.png" alt="Description of final state" width="70%">

## Disclaimer & AI Disclosure
While the **technical architecture, troubleshooting, data migration, and verification** of this lab were performed entirely by the author, **Generative AI** was utilized as a collaborative tool to assist in the structured formatting, professional terminology refinement, and documentation of this report. 

This approach was taken to ensure the lab's technical findings are communicated with the clarity and professional standards required in a production IT environment.
