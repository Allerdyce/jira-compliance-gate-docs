# Atlassian Marketplace Listing Copy — Definition of Done & Subtask Compliance Gate for Jira

- **App Name:** `Definition of Done & Subtask Compliance Gate for Jira`
- **App Key:** `com.evidencepair.jira.compliance.gate`
- **Tagline / Summary (126 chars):**
  `Block Jira resolution transitions until mandatory Definition of Done items are SHA-256 signed off and subtasks are complete.`
- **Categories:** Workflow, Compliance & Security, Project Management, IT & Helpdesk

---

## Highlight 1: Interactive Definition of Done Checklist & SHA-256 Release Seal
- **Title:** `Interactive Definition of Done Checklist & SHA-256 Release Seal`
- **Body:** `Check off mandatory Definition of Done controls with PR/CI/QA verification evidence links directly on Jira issues and lock a tamper-evident SHA-256 release attestation stored in native Jira Issue Properties (<32 KB).`

## Highlight 2: Workflow Transition Validator for DoD & Open Subtasks
- **Title:** `Workflow Transition Validator for DoD & Open Subtasks`
- **Body:** `Automatically block resolving or releasing Jira issues when mandatory Definition of Done items are unchecked, the SHA-256 seal is invalidated, or child subtasks remain open.`

## Highlight 3: Space DoD Template Builder & 1-Click SOC2 / ISO CSV Audit
- **Title:** `Space DoD Template Builder & 1-Click SOC2 / ISO CSV Audit`
- **Body:** `Configure space-level Definition of Done templates, required evidence note rules, and subtask gates with a live Release & Compliance Audit Radar and 1-click RFC-4180 CSV export.`

---

## Full Marketplace Description

**Eliminate premature ticket closures and unverified production releases in Jira and Jira Service Management.**

**Definition of Done & Subtask Compliance Gate for Jira** enforces a cryptographic Definition of Done (DoD) and child subtask completion gate directly inside Jira workflows:

- **Native Jira Workflow Validator (`jira-compliance-dod-validator`)**: Blocks issue transitions to *Resolved*, *Done*, or *Released* (`BLOCKED_INCOMPLETE_DOD_OR_SUBTASKS`) until every mandatory Definition of Done item is checked, required PR/CI/QA evidence is recorded, and 100% of child subtasks are complete.
- **Deterministic SHA-256 Release Sign-Off Seal (`jira-compliance-gate-panel`)**: Computes a verifiable SHA-256 signature over `accountId|issueKey|completedItemIds|subtasksComplete|timestamp|decision`. Unchecking any item after sealing immediately invalidates the signature and re-locks the transition gate.
- **Space DoD Template Builder & Audit Radar (`jira-compliance-gate-admin`)**: Customize mandatory DoD controls per project and export a 1-click SOC2 / ISO 27001 compliance CSV ledger.
- **100% Runs on Atlassian (Zero Data Egress)**: Powered by Forge `nodejs24.x` with zero external servers and zero Forge SQL/KVS—storing all data in native Jira Project & Issue Properties (`<32 KB`).
