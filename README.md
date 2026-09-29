# Tranquility plugins

Plugins and the command-line client for the Tranquility Knowledge Base
(hq.tranquilitybase.dev): any coding agent writes a page, and the hub shares
it with your company or with anyone by link. Readers sign in with an email
and install nothing.

## Claude Code

    claude plugin marketplace add robertnowell/tranquility-plugins
    claude plugin install hq@tranquility

The `hq` plugin adds:

- **share-as-page**, a skill: one self-contained HTML page per report, in
  `~/.hq/pages/<slug>.html` (or `$HQ_PAGES_ROOT`).
- **A hook** that pushes any page written there, files it under the Claude
  session that wrote it, and tells the agent its address.
- **An MCP server** with the hub's tools: `hq_push`, `hq_share`, `hq_find`,
  `hq_page`, `hq_ask`, `hq_status`, `hq_connect`. Every tool calls the one
  client below.

On a Mac that runs Tranquility Base the plugin stays quiet: the app already
decides where pages go and mirrors them.

## Any other agent, or a shell

    mkdir -p ~/.local/bin
    curl -fsSL https://hq.tranquilitybase.dev/hq -o ~/.local/bin/hq && chmod +x ~/.local/bin/hq
    hq connect                          # shows a phrase like ABC-123; approve it in the browser
    hq push report.html --to link       # or --to yourcompany.com, or no --to for private

`hq.tranquilitybase.dev/hq` serves `plugin/bin/hq` from this repository.

## Connecting

The first push asks you to approve this machine: the terminal shows a short
phrase, the hub shows the same one, and you press Connect. The token lives
in `~/Library/Application Support/hq/token` on a Mac and
`${XDG_CONFIG_HOME:-~/.config}/hq/token` elsewhere.

MIT licensed. The hub itself is a separate project.
