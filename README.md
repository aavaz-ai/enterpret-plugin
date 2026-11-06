# Enterpret plugins for Claude Code

A Claude Code plugin marketplace published by [Enterpret](https://www.enterpret.com). `aavaz-ai` is Enterpret's GitHub organization.

## Plugins

| Plugin | What it adds |
|---|---|
| `enterpret` | The Enterpret MCP server (`https://wisdom-api.enterpret.com/server/mcp`). Sign in with your Enterpret account when Claude Code asks; the organization comes from that sign-in. |
|  | Skill `taxonomy-scope`: how to count feedback with `resolve_taxonomy_scope`. A copy of the server's `wisdom://skills/taxonomy-scope` (wisdom-v2 `main`, `taxonomy_scope_skill.py`). The tool itself appears only for sessions the server's `taxonomy_scope_on_mcp` flag admits; the skill says to ignore it otherwise. |

## Install

```
/plugin marketplace add aavaz-ai/enterpret-plugin
/plugin install enterpret@enterpret
```

Using the plugin needs an Enterpret account. Privacy policy: https://www.enterpret.com/privacy-and-policy

Tools and their descriptions are served by the MCP server per session, behind the server's feature flags. Keep `skills/taxonomy-scope/SKILL.md` in step with `TAXONOMY_SCOPE_SKILL_TEXT` in wisdom-v2 when that changes.
