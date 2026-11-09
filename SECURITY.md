# Security: Definition of Done & Subtask Compliance Gate for Jira

Updated 9 November 2026

How the Atlassian Marketplace app **Definition of Done & Subtask Compliance Gate for Jira**, made by EvidencePair LLC, handles data, what protects it, how we handle vulnerabilities, and which certifications apply. What the app stores is listed in full in its [privacy policy](./PRIVACY_POLICY.md).

## Data handling

- **Forge only.** The app runs on Atlassian Forge (`nodejs24.x`) on Atlassian infrastructure.
- **No egress.** The manifest declares no external permissions and no remote services. The app makes requests only to your site's Jira APIs, and it loads no analytics, error-reporting services or external assets.
- **No storage of its own.** The app keeps its data in two Jira entity properties on your site (`complianceGateTemplate` on a project, `complianceGateState` on an issue). It uses no Forge storage or Forge SQL, and EvidencePair has no copy.
- **Requests run as the user where there is one.** The app's screens call Jira as the person using them, so Jira applies that person's own permissions. The workflow validator runs without a signed-in user, so it reads, as the app, the issue and the two properties. It writes nothing.
- **Permissions it asks for.**
  - `read:jira-work`: read issues, the project's recent issues and the two properties.
  - `write:jira-work`: save a checklist to its issue.
  - `manage:jira-project`: save the project's template.
  - `read:app-data:jira`, `write:app-data:jira`: declared but not used by this version.
- **What the checksum is.** A sealed checklist carries a SHA-256 checksum of the account ID, issue key, ticked item IDs, subtask result, time and decision. It shows whether those stored values still match what was sealed. It does not cover the evidence notes. It is not a digital signature: someone with permission to edit the issue property could change the record and recompute the checksum.

## Encryption

The app stores nothing outside your Jira site and sends nothing outside Atlassian's platform. Encryption in transit and at rest is provided by Atlassian as part of your site, as described in the [Atlassian Trust Center](https://www.atlassian.com/trust). The app adds no encryption of its own.

## Vulnerability management

- **Reporting.** Email security@evidencepair.com. Tell us the app, what you found and how to reproduce it. Please do not test against sites you do not own. We acknowledge every report within one business day.
- **Response.** EvidencePair adopted a written security incident response plan on 12 October 2026. It covers triage, containment, investigation, notification of Atlassian and affected customers, and recovery.
- **Dependencies.** The app's npm dependencies are pinned in its lockfile. Atlassian maintains and patches the Forge runtime.
- **Bug bounty.** We do not run a bug bounty programme.

## Certifications

EvidencePair holds no security certifications, and the app has had no independent penetration test or external audit. The infrastructure the app runs on is Atlassian's, and Atlassian's own certifications cover it: see the [Atlassian Trust Center](https://www.atlassian.com/trust).
