# Definition of Done & Subtask Compliance Gate for Jira

**App Key:** `com.evidencepair.jira.compliance.gate`  
**App ID:** `ari:cloud:ecosystem::app/658bb960-1d22-4014-8b23-e491468b4e68`  
**Vendor:** EvidencePair LLC (`support@titlecovenant.com`)  
**Runtime:** Atlassian Forge `nodejs24.x` (100% *Runs on Atlassian*, Zero External Remotes, Zero Forge SQL/KVS)

---

## Overview

**Definition of Done & Subtask Compliance Gate for Jira** blocks premature Jira issue resolution and release transitions until all mandatory Definition of Done (DoD) items are cryptographically signed off with a deterministic **SHA-256 Release Seal** and 100% of child subtasks are complete.

1. **Space DoD Template & Subtask Rule Engine (`jira-compliance-gate-admin`)**: Configure mandatory Definition of Done controls (e.g., *Peer Code Review Verified*, *Security & Dependency Scan Clean*, *QA Regression Passed*, *Rollback & Customer Comms Ready*), required verification evidence links, and strict **Block if Open Subtasks Exist** enforcement in Jira Project Property `complianceGateTemplate` (`<32 KB`).
2. **Interactive Issue DoD Checklist & SHA-256 Attestation Seal (`jira-compliance-gate-panel`)**: Check off mandatory DoD controls with PR/CI/QA evidence links and click **Seal & Attest Definition of Done** to generate a deterministic SHA-256 signature (`accountId|issueKey|completedItemIds|subtasksComplete|timestamp|decision`) stored in Jira Issue Property `complianceGateState` (`<32 KB`). Unchecking any item immediately invalidates the seal.
3. **Workflow Transition Validator & SOC2 / ISO 27001 CSV Export (`jira-compliance-dod-validator`)**: Automatically blocks issue resolution transitions (`BLOCKED_INCOMPLETE_DOD_OR_SUBTASKS`) unless a verified SHA-256 release seal (`CLEARED_SHA256_SEAL_VERIFIED`) is present and all subtasks are closed. Includes a space-wide **Release & Compliance Audit Radar** with 1-click CSV export.

---

## Documentation Links

- [User Guide & Administration Manual](./USER_GUIDE.md)
- [Privacy, Data Residency & Security Policy](./PRIVACY_AND_SECURITY.md)
- [End-User License Agreement (EULA)](./EULA.md)
- [Atlassian Marketplace Listing Copy](./LISTING_COPY.md)
- [Progressive Cloud Pricing Table](./PRICING_TABLE.md)
