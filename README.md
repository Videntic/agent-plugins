# Videntic plugin marketplace

This repository distributes Videntic's Claude plugin: four workflows for
connecting your Workspace, preparing an AI Visibility brief, comparing tracked
Competitors, and investigating Technical Audit evidence. It connects to the
hosted Videntic MCP service using OAuth and your existing Project permissions.

This repository provides public setup instructions and installable plugin
files. The plugin is not yet listed in the Claude Directory; review and
publication are separate from installing it from this repository.

Install in Claude Code:

```bash
claude plugin marketplace add Videntic/agent-plugins
claude plugin install videntic@videntic
```

Open /mcp and sign in to Videntic. Then ask: Connect Videntic and list my accessible Projects.

See [the plugin guide](plugins/videntic/README.md) for workflows, examples, permissions, and support.

The directory submission uses `plugins/videntic` as the plugin path and `main`
as the tracked branch. This repository contains distribution files only; the
Videntic backend and customer data are not included. The MIT license applies to
the plugin instructions and packaging files, as described in LICENSE.
