# Retail inMotion Smart Approval Manager for JSM

> **Retail inMotion edition.** Internal app for the Retail inMotion work site (`retailinmotion.atlassian.net`) and sandbox (`retailinmotion-sandbox1.atlassian.net`). It is a separate repository and Forge app from the Marketplace edition and is not published to the Atlassian Marketplace.
>
> Before the first deploy: run `forge register "Retail inMotion Smart Approval Manager"`, put the printed id in `manifest.yml` (`app.id`), and add the `FORGE_EMAIL` / `FORGE_API_TOKEN` secrets. Merges deploy to the sandbox as before; the work site is deployed only by the manual **Deploy to Retail inMotion work site** workflow. The **Brand check** workflow fails if the Marketplace brand appears anywhere in the repository.

A Forge app that makes customer approvals simple for Jira Service Management agents, project admins and portal customers.

## What it does

### Agent
1. Open a JSM ticket and open **Smart Approval**.
2. Review approvers prepared by a matching rule, or search and select approvers manually.
3. Choose whether **all approvers** or **any one approver** is enough.
4. Add or review the decision message.
5. Click **Request approval** when ready. Preparation rules never send automatically.
6. Track waiting/approved/declined progress, send reminders or cancel pending approvals from the same panel.

### Customer approver
1. Sign in to the JSM customer portal.
2. See the **My approvals** summary.
3. Open **My Approvals** from the portal user menu.
4. Review every request currently awaiting a decision.
5. Approve or decline and optionally add a decision comment.
6. See previous decisions in approval history.

### Project administrator
1. Open **Smart Approval Manager** in project settings.
2. Configure default reminder, participant and decline behaviour.
3. Choose friendly Jira target statuses for approval requested / approved / declined actions.
4. Create approval preparation rules using the guided rule builder.
5. Match issue type, priority, status or custom-field values.
6. Optionally wait until the ticket reaches a selected workflow status before preparing the approval.
7. Assign one or more approvers and choose **all** or **any** approval logic per rule.

## V1 capabilities

- Agent-side approval request panel
- Customer portal My Approvals inbox
- Consent-free customer approval experience
- One or multiple approvers
- All-approvers or any-one approval requirements
- Decision comments and configurable required decline reason
- Group approval progress and audit events
- Manual reminders
- Hourly automatic reminder processing
- Cancel pending approvals
- Automatic request-participant addition when the agent sends
- Visual approval preparation rule builder
- Rules based on Jira/custom-field values
- Optional status-triggered approval preparation
- Agent-controlled send for every rule-prepared approval
- Optional Jira status change when approval is requested
- Optional Jira status change after approval
- Optional Jira status change after decline
- Per-rule workflow overrides
- Per-project configuration
- Forge-hosted storage using `@forge/kvs`
- No external backend or external data store

## Architecture

Smart Approval Manager maintains its own approval records while Jira/JSM remains the system of record for the request. Matching product events can prepare a suggestion in Forge storage; an agent must explicitly request the approval before participants, comments or workflow actions are applied. Customer decisions are authorised against the assigned Atlassian account ID before Jira-side actions are performed.

## Development validation

```bash
npm install
npm test
forge lint
forge deploy -e development
```

Install and test on a non-production Jira Service Management site before production deployment.

See `docs/TEST-PLAN.md`, `docs/MARKETPLACE.md` and `docs/SECURITY-PRIVACY.md` for the release pack.
