# Privacy policy: Definition of Done & Subtask Compliance Gate for Jira

Updated 9 November 2026

This policy describes the Atlassian Marketplace app **Definition of Done & Subtask Compliance Gate for Jira** ("the app"), made by EvidencePair LLC ("EvidencePair", "we"). EvidencePair's company privacy policy, which covers our website and email you send us, is at <https://evidencepair.com/privacy/>.

## In short

- The app runs on Atlassian Forge, inside your Jira site. It declares no external egress and no remote services, and it makes requests only to your site's Jira APIs.
- It keeps its data in Jira itself, as two Jira entity properties. That data is never sent to EvidencePair.
- The only personal data it stores itself is the Atlassian account ID of the last person who saved or sealed an issue's checklist, plus whatever people type into the checklist's evidence fields.

## What the app stores

**One project property, `complianceGateTemplate`, per project where someone saved the template on the app's project page:**

- the project's ID, and a project key field. This version always saves `ITH` there, the key from the app's built-in default template;
- three rules: whether the workflow validator blocks transitions, whether open subtasks block sealing and transitions, and whether evidence notes are required;
- the checklist items: for each, an ID, a title, a category, a description, and whether it is mandatory and needs evidence. Unless someone has changed the property through Jira's REST API, these are the app's four built-in items;
- a list of issue type names, which the app stores but does not use;
- a list of simulated open subtasks for testing, which stays empty unless someone adds entries through Jira's REST API;
- when the template was last saved, and the size of the saved record.

**One issue property, `complianceGateState`, per issue where someone ticked or unticked a checklist item, or sealed the checklist:**

- the issue key and the project ID;
- the Atlassian account ID of the person who last saved it, and when;
- which checklist items are ticked;
- the evidence notes, one per item, as typed. The panel fills these fields with example text, such as a made-up pull request number, until someone changes it, and the app saves whatever the fields contain;
- whether the checklist is sealed, and its decision: approved for release, or an unsealed draft;
- whether the issue's subtasks were complete when it was sealed;
- for a sealed checklist, a SHA-256 checksum of the account ID, issue key, ticked item IDs, subtask result, time and decision, and the formula used to compute it. The checksum lets the app tell whether those values have changed since sealing. It adds no information of its own, and it does not cover the evidence notes;
- the size of the saved record.

Each save replaces the issue's previous record, so the app keeps no history. Ticking or unticking an item after sealing replaces the sealed record with an unsealed draft.

The app does not look up names, email addresses or profiles. Evidence notes can contain personal data, and the app stores them exactly as entered.

## What the app reads from Jira

- The issue or project the app is opened from.
- For each issue it checks, the whole issue: the app does not limit the fields it asks Jira for. It uses only the summary, issue type, status and subtasks (each subtask's key, summary and status). Jira's response also contains the issue's other fields, such as its description. The app does not use, store or log them.
- The two properties above.
- On the project page, the 15 most recently created issues in the project, each read as above, to show their checklist status. If that search finds no issues, the page shows issue key `ITH-1` from the app's test configuration instead, and reads that issue on your site if one exists.
- When the workflow validator runs on a transition: the issue, its `complianceGateState` property and its project's `complianceGateTemplate` property.

## Where the data lives

Entity properties are part of your Jira site's data. Atlassian stores them with the rest of your site, in your site's data residency location, under Atlassian's own security and privacy commitments. The app has no storage of its own: it uses no Forge storage and no Forge SQL, and EvidencePair runs no servers in its path.

## Who can see it

Jira shows an entity property to anyone who can view the issue or project it belongs to, through Jira's REST API. Anyone who can see an issue can therefore read its checklist record, including the account ID and the evidence notes. The issue panel shows the account ID of the person who sealed the checklist. The project page shows a CSV of its 15 most recent issues that includes the account ID in each issue's record, to anyone who can open the page. Jira's permissions also decide who can change the properties: changing an issue property needs permission to edit the issue, and changing a project property needs permission to administer the project.

## Retention and deletion

The app keeps both properties until someone deletes them. It has no retention setting, runs no scheduled jobs, deletes nothing on its own, and has no uninstall step. Deleting an issue deletes its properties. A Jira administrator can delete either property at any time through Jira's REST API, and should do so before uninstalling if the data must go. The CSV on the project page is built each time the page loads, and the app does not store it.

## Account closure

The app does not take part in Atlassian's personal data reporting. When an Atlassian account is closed, its account ID stays in any checklist record that person last saved, until that property, or the issue, is deleted.

## Platform logs

The app writes nothing to the Forge platform's logs. Atlassian's platform can still record errors it sees while the app runs, such as an unhandled error and its message ([Atlassian: view app logs](https://developer.atlassian.com/platform/forge/view-app-logs/)). The error messages the app raises itself contain at most an issue key, the titles of checklist items and the size of a record.

## Email and support

If you email us, our [company privacy policy](https://evidencepair.com/privacy/) describes how we handle that email, and the current restrictions on where our apps may be used.

## What we never do

We do not sell personal data or use it for unrelated advertising or AI training. The app's data stays in your Jira site and never reaches us.

## Changes to this policy

The date at the top changes when this policy does. Every version is kept in this repository's history.

## Contact

hello@evidencepair.com
