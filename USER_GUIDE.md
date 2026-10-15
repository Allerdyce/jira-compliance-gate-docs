# User Guide — Definition of Done & Subtask Compliance Gate for Jira

## 1. Quick Start & Installation

1. Install **Definition of Done & Subtask Compliance Gate for Jira** (`com.evidencepair.jira.compliance.gate`) from the Atlassian Marketplace onto your Jira or Jira Service Management Cloud site.
2. Navigate to **Project Settings → Apps → DoD Templates & Compliance Audit** (`jira-compliance-gate-admin`) to review or customize your space's mandatory Definition of Done checklist and child subtask enforcement rules.
3. Attach the **Definition of Done & Subtask SHA-256 Validator** (`jira-compliance-dod-validator`) to your workflow's *Resolve* / *Done* / *Release* transitions under **Project Settings → Workflows**.

---

## 2. Configuring Space Definition of Done Templates (`jira:projectPage`)

In **DoD Templates & Compliance Audit**, project administrators configure:
- **Strict Workflow Validator Gate (`strictWorkflowBlocking`)**: Enforces hard transition blocking via `jira-compliance-dod-validator`.
- **Block if Open Subtasks Exist (`blockIfOpenSubtasks`)**: Requires all child subtasks on an issue to be in the `done` status category before the parent issue can be sealed or resolved.
- **Require Verification Evidence Notes (`requireEvidenceNotes`)**: Requires engineers to attach a PR link, CI run URL, or QA test reference on mandatory items.
- **Mandatory DoD Items**:
  1. `Peer Code Review Verified` (`dod-peer-review`)
  2. `Security & Dependency Scan Clean` (`dod-sec-scan`)
  3. `QA Regression Passed` (`dod-qa-regression`)
  4. `Rollback & Customer Comms Ready` (`dod-rollback-comms`)

All space rules are stored in native Jira Project Property `complianceGateTemplate` (`/rest/api/3/project/{projectId}/properties/complianceGateTemplate`, `<32 KB`).

---

## 3. Sealing & Attesting an Issue's Definition of Done (`jira:issuePanel`)

1. Open any Jira issue and expand the **Definition of Done & Compliance Gate** panel (`jira-compliance-gate-panel`).
2. Check off each mandatory Definition of Done control and enter verification evidence (e.g., PR number, Snyk/Semgrep scan run, Playwright E2E build).
3. Ensure all child subtasks are completed (`0 OPEN SUBTASKS`).
4. Click **Seal & Attest Definition of Done (SHA-256)**.
5. The app computes a deterministic SHA-256 digest over:
   `accountId|issueKey|completedItemIds|subtasksComplete|timestamp|decision`
   and persists the sealed record to Jira Issue Property `complianceGateState` (`<32 KB`).
6. The workflow transition gate immediately updates to `CLEARED_SHA256_SEAL_VERIFIED`. If any item is subsequently unchecked, the seal is automatically invalidated and reverts to `BLOCKED_INCOMPLETE_DOD_OR_SUBTASKS`.

---

## 4. Exporting SOC2 / ISO 27001 Compliance Audit CSV

In **DoD Templates & Compliance Audit**, review the **Space Release & Compliance Audit Radar** table and copy or download the RFC-4180 escaped CSV containing issue keys, DoD completion counts, subtask states, attesting Account IDs, UTC timestamps, and 64-character SHA-256 release seals.

---

## 5. Support & Contact

- **Vendor:** EvidencePair LLC
- **Support & Security Email:** `support@titlecovenant.com`
- **SLA:** 1 Business Day response for all customer inquiries.
