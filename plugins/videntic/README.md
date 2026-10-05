# Videntic

Understand your Project's AI Visibility using measured analytics, Brand Mentions,
Citations, and Technical Audit evidence. Videntic connects through an
OAuth-protected remote MCP server at `https://mcp.videntic.com/mcp`.

## Connect your Workspace

You need a Videntic account and access to a Project. Enable the plugin in your
client, open its MCP manager, and authenticate Videntic in the browser. Select
the Workspace and action permissions you want to grant. Your existing Project
permissions still apply. Never paste your password or an API key into chat.

For Claude Code, load the distributed Claude package with:

```bash
claude --plugin-dir ./videntic
```

Then open `/mcp` and authenticate Videntic. You can also connect the hosted server
directly without installing a plugin:

```bash
codex mcp add videntic --url https://mcp.videntic.com/mcp
codex mcp login videntic

claude mcp add --transport http --scope user \
  videntic https://mcp.videntic.com/mcp
```

## Start with one successful read

Ask: **“Connect Videntic and list my accessible Projects.”** Choose the Project
you want to investigate. The assistant confirms its Website and Market before
producing a report. An empty Project list calls for checking your Workspace and
Project access. Missing measurements stay unavailable; the assistant will not
silently start a billed Analysis to fill the gap.

## Get a useful report

| Ask | What you receive | Example |
| --- | --- | --- |
| “Write an AI Visibility brief for my Project, comparing the latest two comparable Analyses.” | Measured Metrics, changes, selected evidence, limitations, and next steps | [Synthetic brief](skills/analyze-ai-visibility/references/example-report.md) |
| “Compare my Brand with its tracked Competitors and explain the strongest gaps.” | Measured comparison, current tracking status, Citation evidence, and a supported next step | [Synthetic comparison](skills/compare-competitors/references/example-report.md) |
| “Investigate my latest Technical Audit and prioritize Findings with affected-page evidence.” | Anchored Audit Run, prioritized Findings, observed/expected values, and an implementation handoff | [Synthetic investigation](skills/investigate-technical-audit/references/example-report.md) |

These examples contain fictional data. Reports use your actual returned
measurements and explain incomplete evidence. A snapshot comparison is not a
weekly aggregate, and a tracked Prompt's observation count is not search demand.

The workflows can be selected automatically. In Claude Code, you can also invoke
`/videntic:connect-videntic`, `/videntic:analyze-ai-visibility`,
`/videntic:compare-competitors`, or `/videntic:investigate-technical-audit`.
Request a Markdown file if you want to save the report; the bundled templates
guide its structure. Existing Videntic PDF-report tools expose metadata, not a
PDF download.

For Technical Audit remediation, the agent reads an anchored Audit Run and
compares its evidence with your current Website. It can guide changes in
WordPress, Webflow, another CMS or site builder, or your source repository.
GitHub access is not required. Editing requires a separately available tool
and your authorization; otherwise you receive an implementation handoff.
Videntic MCP tools do not edit or publish your Website. Verify published changes
with a later comparable Audit Run in Videntic.

## If something is missing

- **Sign-in fails:** reconnect Videntic from your client's MCP manager.
- **Project access is denied:** check Workspace selection and ask your admin
  to review Project access; reconnecting alone does not grant permission.
- **No finalized Analysis:** run Analysis in Videntic or explicitly request
  the supported billed action after checking allowances.
- **No Audit Runs:** start a Technical Audit in Videntic before requesting
  Findings. An unavailable overview is not proof of a clean audit.
- **Search volume, publishing, or verified resolution is requested:** these
  workflows cannot supply those results; the assistant explains the supported
  next action without inventing evidence.

## Project actions and data handling

The server also supports consented Project actions, including managing Prompts
and Competitors, editing Perception Questions, requesting Analysis, configuring
supported Analysis schedules, and creating or editing local Content Drafts.
Every action requires your intent, capability consent, and current permissions.
Analysis and draft creation consume Plan allowances. The plugin does not publish
content. A queued operation is not a completed result.

Project information returned by tools is shared with the AI client you connect.
The client sends tool arguments and authorized writes to
`https://mcp.videntic.com/mcp`; OAuth sign-in uses Videntic's authorization
service in your browser. The hosted service records tool-usage telemetry in
PostHog, including stable actor/client identifiers, available model metadata,
bounded outcomes, and operation metadata. Raw tool parameters, API responses,
request headers, private error messages, conversation identifiers, and automatic
conversation summaries are excluded from that analytics stream. If you explicitly
agree to report a missing capability, the service records your general capability
description as feedback; never include personal information, credentials, or
customer content in it. This redaction does not mean the service
does not process the inputs needed to perform your requested operation.
The bundle runs no local server, lifecycle hooks, or installation scripts.
When you request repository remediation or a saved report, your assistant uses
its own local file tools and the repository's checks; that may read or change
the files you authorized it to work on.
MCP Cloud Logging records are retained for 30 days; the central API log export
uses 90-day retention. PostHog analytics events and saved Project records can
remain longer than 30 days. PostHog's standard event retention is plan-based
(one year free, seven years paid). See the privacy policy for processing,
retention, and deletion requests.

The package itself stores no credentials or customer data. You can revoke the
connection or its grants in Videntic. Review the
[privacy policy](https://www.videntic.com/privacy-policy) and
[service terms](https://www.videntic.com/terms-of-service) before connecting.
For help, [contact Videntic](https://www.videntic.com/contact).

The plugin files are MIT licensed. This license does not cover the hosted
Videntic service or customer data, and does not grant trademark rights in the
Videntic name or logo.
