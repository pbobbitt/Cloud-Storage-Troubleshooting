# Technical Implementation Log

This document provides a step-by-step technical record of the project phases. It is intended for technical review, auditing, and reproducibility.

---

#### Phase 1: Questioning the User / Storage Audit
User described their issue of having nearly maxxed out storage they gave me access to their desktop and after talking with them they were just wanted to free cloud space but still wanted to keep access to any data. they think that they just had alot of old files but had no idea what the make up or ratio of that data may have been.

user granted me access to their windows 11 desktop to troubleshoot. my first step was to open https://one.google.com/ to see what was taking up the most space. once viewing the result it turned out that the bulk of data was from google drive. I spoke with the user, and after a bit of back and forth, they were ok with deleting or archiving data. 
* **Observation:** Most of the data is taken by google drive
* **Strategic Decision:** seems like a simple fix just need to export this data and archive to a physical drive on the same desktop.

> **Evidence:** See [Before Storage Audit](https://github.com/pbobbitt/SaaS-Storage-Optimization-Data-Lifecycle-Management-Lab/blob/main/Images/Before%20Storage%20Audit) in Visual Documentation.

#### Phase 2: Design & Configuration Strategy
Established the technical parameters and safety protocols before executing changes.
* **Parameters:** [e.g., Static IP assignments, RAID levels, or Volume Chunking sizes.]
* **Fault Tolerance Strategy:** [Explain how you protected against failure during the process. e.g., "Created a system restore point" or "Segmented downloads to prevent packet loss corruption."]

#### Phase 3: Deployment & Execution
Initiated the core technical work, moving from the planning phase to active implementation.
* **Workflow:** [Describe the sequential steps taken. e.g., "Executed a clean install of the OS" or "Initiated the data migration from SaaS to Local."]
* **Infrastructure Check:** [Describe the pre-flight check. e.g., "Verified destination disk health using CHKDSK."]

#### Phase 4: Integration & Archival
Organized the environment for long-term stability and performance.
* **Action:** [e.g., "Moved verified assets from Staging to Production" or "VLAN tagging to isolate guest traffic."]
* **Technical Justification:** [Why this step matters for performance. e.g., "Separating OS traffic from Data traffic to prevent bottlenecking."]

#### Phase 5: Risk Mitigation & Remediation
Executed the final "Cleanup" or "Cut-over" to restore service or clear the original issue.
* **Safety Configuration:** [How did you ensure the fix didn't break something else? e.g., "Disabled bidirectional sync to prevent accidental cloud deletion."]
* **Administrative Action:** [The "Heavy Lifting" step. e.g., "Purged legacy data" or "Replaced the faulty CMOS battery."]
* **Result:** [The immediate outcome. e.g., "Recovered 50% capacity" or "System successfully passed POST."]

> **Evidence:** See [Post-Action/Verification Screenshot] in Visual Documentation.

#### Phase 6: System Hardening & Preventative Maintenance
Applied optimization settings to ensure the fix lasts and the system is more resilient than before.
* **Action:** [e.g., "Updated firmware to latest version" or "Changed upload policy to Storage Saver."]
* **Technical Justification:** [Explain the 'Optimization' logic. e.g., "Reducing bitrate velocity to extend the lifespan of the storage tier."]

#### Phase 7: Infrastructure Redesign & Orchestration
The "Pro" step: Re-architecting the system to prevent the problem from ever happening again.
* **Service Redirection:** [How you changed the flow of data or traffic. e.g., "Redirected backups to a secondary node."]
* **IAM/Access Management:** [Who or what has access now? e.g., "Configured Partner Sharing for unified access."]
* **Final Result:** [The high-level win. e.g., "Established a scalable architecture that adheres to the Principle of Least Privilege."]

---
*End of Implementation Log*
