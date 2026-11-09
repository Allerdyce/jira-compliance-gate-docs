# Privacy, Data Residency & Security Architecture — Definition of Done & Subtask Compliance Gate for Jira

> The app's privacy policy is [PRIVACY_POLICY.md](./PRIVACY_POLICY.md), and its security documentation (data handling, encryption, vulnerability management and certifications) is [SECURITY.md](./SECURITY.md). This page is the architecture summary.

**Updated:** 9 November 2026  
**App Key:** `com.evidencepair.jira.compliance.gate`  
**Vendor:** EvidencePair LLC  
**Support:** <https://evidencepair.com/support/> (`support@evidencepair.com`)  
**Security Contact:** `security@evidencepair.com`

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

Because all data resides inside Jira entity properties, Atlassian stores it with the rest of your Jira site, in your site's data residency location. Encryption in transit and at rest is Atlassian's, as part of your site, as described in the [Atlassian Trust Center](https://www.atlassian.com/trust).

---

## 3. Personal Data

- **No Personal Data Stored Externally**: The app does not collect, export, or store personal data (names, email addresses, IP addresses, or payment information) outside your Jira instance.
- **Atlassian Account ID**: When a user ticks or unticks a Definition of Done checklist item, or seals the checklist, their opaque Atlassian `accountId` (e.g., `712020:...`) and a UTC timestamp are recorded inside the issue's `complianceGateState` property. Each save replaces the previous record, so it holds only the most recent person. On a sealed checklist, the account ID is part of the SHA-256 checksum.
- **Evidence Notes**: The verification evidence typed into the issue panel is stored as entered in `complianceGateState`, and can contain personal data.
- **Deletion**: Deleting a Jira issue deletes its `complianceGateState` property. The app deletes nothing itself and has no uninstall step. A Jira administrator can delete either property at any time through Jira's REST API.
- **Account Closure**: The app does not take part in Atlassian's personal data reporting. A closed account's ID stays in any record that person last saved until the property or the issue is deleted.

---

## 4. Scopes

| Scope | Justification |
|---|---|
| `read:jira-work` | Read issues (the app uses the summary, status, issue type and child subtasks), the project's recent issues, and the project/issue compliance properties. |
| `write:jira-work` | Persist per-issue Definition of Done checklist & SHA-256 attestation seal in `complianceGateState`. |
| `manage:jira-project` | Persist space-level Definition of Done templates & subtask rules in `complianceGateTemplate`. |
| `read:app-data:jira` | Declared but not used by this version. |
| `write:app-data:jira` | Declared but not used by this version. |

---

## 5. Security Contact & Vulnerability Disclosure

To report a security issue, email `security@evidencepair.com`. We acknowledge every report within one business day. EvidencePair holds no security certifications; see [SECURITY.md](./SECURITY.md).
