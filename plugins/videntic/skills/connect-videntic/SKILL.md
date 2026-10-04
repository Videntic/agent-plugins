---
name: connect-videntic
description: Connect Videntic, check accessible Projects, and help a new user choose their first AI Visibility or Technical Audit workflow. Use for setup and connection troubleshooting, not a full report.
---

# Connect Videntic

Help the user reach one successful read without changing Project data.

1. If Videntic tools are unavailable, explain that they must enable the plugin
   and authenticate its MCP connection in their client's MCP manager. The hosted
   endpoint is `https://mcp.videntic.com/mcp`. Sign-in happens in the browser;
   never ask for a password, token, or Public API key in chat.
2. Call `list_projects`. Follow its cursor if the requested Project is not on
   the first page. Resolve only returned opaque IDs. Select the user's named
   Project; if several match, ask which one. With no selection and several
   Projects, show names and Websites and ask; do not default to the first one.
3. Call `get_project` for the selected ID. Confirm its Website, Market, and
   latest Analysis time. An empty accessible set means there is nothing this
   connection can read; suggest checking the selected Workspace and Project
   access in Videntic. Do not try another Workspace without the user's choice.
4. Offer the first task using the confirmed Project: an AI Visibility brief,
   a Competitor comparison, or a Technical Audit investigation. If the user
   already requested one, continue to the matching skill directly. A missing
   Analysis does not prevent investigation of an existing Technical Audit.

For an authentication failure, direct the user to reconnect. For `forbidden`,
explain that sign-in alone does not grant Project access. Ask the user to check
their Workspace selection or have an admin adjust access. A rate limit calls
for the server's suggested delay, not reconnection. Report the bounded error
code and next useful action without exposing credentials or private error text.

Finish with the selected Project and the successful connection check. Do not
claim analytics are available until they have been read. Report generation
uses existing data; it does not automatically start billed Analysis or create
Content Drafts.
