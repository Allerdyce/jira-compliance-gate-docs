# Privacy, Data Residency & Security Policy — Definition of Done & Subtask Compliance Gate for Jira

**Effective Date:** October 15, 2026  
**App Key:** `com.evidencepair.jira.compliance.gate`  
**Vendor:** EvidencePair LLC (`support@titlecovenant.com`)

---

## 1. 100% Runs on Atlassian & Zero External Data Egress

**Definition of Done & Subtask Compliance Gate for Jira** is built exclusively on the Atlassian Forge `nodejs24.x` runtime (`arm64`) with **zero external `remotes:`** and **zero third-party network egress**. All code execution occurs 100% within Atlassian's managed Forge compute infrastructure.

---

## 2. Zero-Cost Host Entity Property Persistence (`<32 KB` Enforced)

The app does **not** use external databases, Forge SQL, or Forge KVS. All configuration and attestation state is stored directly in your Jira Cloud instance's native Entity Properties:

- **Project Template Property (`complianceGateTemplate`)**:
  `/rest/api/3/project/{projectIdOrKey}/properties/complianceGateTemplate` (`<32 KB` enforced via `assertPropertyPayloadUnder32KB`)
- **Issue Attestation Property (`complianceGateState`)**:
  `/rest/api/3/issue/{issueKey}/properties/complianceGateState` (`<32 KB` enforced via `assertPropertyPayloadUnder32KB`)

Because all data resides inside Jira Host Entity Properties, your compliance data automatically inherits your Atlassian Jira Cloud tenant's **Data Residency**, backup/restore lifecycle, encryption at rest (AES-256), and encryption in transit (TLS 1.2+/1.3).

---

## 3. Personal Data & GDPR Compliance

- **No Personal Data Stored Externally**: The app does not collect, export, or store personal data (names, email addresses, IP addresses, or payment information) outside your Jira instance.
- **Pseudonymous Atlassian Account ID Only**: When a user seals a Definition of Done checklist, only their opaque Atlassian `accountId` (e.g., `712020:...`) and UTC timestamp are recorded inside the issue's `complianceGateState` property for cryptographic non-repudiation.
- **Automatic Deletion**: Deleting a Jira issue or project immediately and permanently deletes its associated `complianceGateState` and `complianceGateTemplate` entity properties.

---

## 4. Least-Privilege Scopes

| Scope | Justification |
|---|---|
| `read:jira-work` | Read issue summary, status, issue type, child subtasks, and project/issue compliance properties. |
| `write:jira-work` | Persist per-issue Definition of Done checklist & SHA-256 attestation seal in `complianceGateState`. |
| `manage:jira-project` | Persist space-level Definition of Done templates & subtask rules in `complianceGateTemplate`. |
| `read:app-data:jira` | Read app-scoped Jira entity metadata. |
| `write:app-data:jira` | Write app-scoped Jira entity metadata. |

---

## 5. Security Contact & Vulnerability Disclosure

To report a security issue or request a SOC2 / ISO 27001 architecture review, contact **EvidencePair LLC Security** at `support@titlecovenant.com`. Critical security reports are acknowledged within **24 hours**.
