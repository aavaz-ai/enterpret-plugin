# Enterpret plugins for Claude Code

A Claude Code plugin marketplace. Private for now.

## Plugins

| Plugin | What it adds |
|---|---|
| `wisdom` | The Enterpret Wisdom MCP server (`https://wisdom-api.enterpret.com/server/mcp`). Sign in with your Enterpret account when Claude Code asks; the organization comes from that sign-in. |

## Install

```
/plugin marketplace add aavaz-ai/enterpret-plugin
/plugin install wisdom@enterpret
```

While the repo is private, installing needs GitHub access to `aavaz-ai/enterpret-plugin`.

Tools, their descriptions and any skills (such as `wisdom://skills/taxonomy-scope`) are served by the MCP server per session, behind the server's feature flags; this plugin only points Claude Code at the server.
