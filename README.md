<p align="center"><img src="icon.png" width="96" alt="Repping.ai logo"></p>

# Repping.ai MCP server and creator content skill

Connect a supported OAuth MCP host to your [Repping.ai](https://www.repping.ai) workspace.
Callback origins must pass the server’s trusted-origin policy. Protocol support alone does not guarantee client compatibility.
Ask about your posts, calendar, [Link in Bio page](https://learn.repping.ai/features/link-in-bio) and analytics.
The assistant prepares changes, and **you approve each change in Repping.ai** before anything runs.

This repo contains:

- **Setup guides** for the remote MCP server at `https://www.repping.ai/api/mcp`
- **A Claude Code plugin** that bundles the server connection and a skill
- **`creator-content-workflow`**, a skill for planning, drafting, adapting and reviewing social posts. It works with or without Repping.ai.

Full product documentation: [repping.ai/mcp](https://www.repping.ai/mcp)

## Quick start

| Client | Setup |
| --- | --- |
| **Claude Code** | `/plugin marketplace add reppingai/repping-mcp`, then `/plugin install repping@repping` |
| **Claude Code (server only)** | `claude mcp add --transport http repping https://www.repping.ai/api/mcp` |
| **Claude (web and desktop)** | Customize → Connectors → Add custom connector → `https://www.repping.ai/api/mcp` → Register automatically |
| **ChatGPT** | Add a custom MCP connector with the server URL and OAuth authentication. Your plan and workspace settings control this option. |
| **Cursor** | Copy [`examples/cursor-mcp.json`](examples/cursor-mcp.json) into `.cursor/mcp.json` |
| **Codex CLI** | Add [`examples/codex-config.toml`](examples/codex-config.toml) to `~/.codex/config.toml` |
| **Other MCP clients** | Streamable HTTP, OAuth 2.1 and PKCE; requires an approved HTTPS callback origin |

The entries above describe configuration formats, not verified compatibility for every client.
Claude Code, Cursor and Codex CLI connections that use localhost callbacks are not supported by the current HTTPS-only policy.
Other hosts need their exact HTTPS callback origin approved by the server operator before registration can succeed.
The standalone creator-content-workflow skill remains usable without an MCP connection.

After a supported host connects, sign in to Repping.ai, choose one workspace and approve the requested access.

## OAuth compatibility and directory health checks

The server restricts OAuth redirects at client registration, authorization and token exchange.
Its default trusted origins are `https://claude.ai`, `https://claude.com`, `https://chatgpt.com` and `https://chat.openai.com`.
Deployments can override this list through `MCP_ALLOWED_REDIRECT_ORIGINS`; the configured list replaces the defaults.
Only exact approved HTTPS origins are accepted. Wildcards, localhost callbacks and arbitrary client origins are not accepted.
Never disable this restriction to make a directory health check pass.

An unauthenticated MCP request can return HTTP 401. That alone does not establish downtime.
Glama requires connector ownership verification and a separate OAuth test profile for authenticated health checks and tool discovery.
Use an isolated test workspace with no private content or connected social accounts.
Review its requested scopes and approve only those needed for inspection.
A server operator must verify the host’s actual callback origin before adding it to the allowlist.
Do not place access tokens, refresh tokens or test credentials in this public repository.

Background analytics synchronization does not invalidate an approved proposal solely through analytics metadata changes.
The server still checks destination authority and resource health before execution.

## Tools

| Tool | What it does |
| --- | --- |
| `repping_profile` | Identifies the connected account and workspace. It returns no email or username. |
| `repping_discover` | Lists data areas, operations and exact input schemas. |
| `repping_read` | Reads posts, the calendar, the Link in Bio page, media, analytics and the credit ledger. |
| `repping_prepare` | Saves one proposed change and returns a review link. It does not publish anything. |
| `repping_action_status` | Shows the status of a prepared change after a person reviews it. |

## Safety model

- OAuth 2.1 with PKCE. You sign in yourself, so the AI app never sees your password.
- Each connection can access only the one workspace you select.
- The assistant can read and prepare. It **cannot approve, publish or run** a change.
- You can revoke any connection under **Settings → MCP** in Repping.ai.
- Reading and preparing through MCP uses no Repping.ai credits.

## Plans

The Creator plan includes MCP access. See [current plans](https://www.repping.ai/pricing).
You can build a [free creator page](https://www.repping.ai/signup) on the Free plan.

## The creator content workflow skill

[`skills/creator-content-workflow`](skills/creator-content-workflow/SKILL.md) turns source material into reviewed, platform-ready posts:

1. Gather the source material (notes, an article, a video transcript)
2. Check every claim against the source
3. Draft one core message
4. Adapt it for each platform's format and limits
5. Review it, then schedule. With Repping.ai connected, the skill prepares drafts that you approve in the app.

Install only the skill: copy the folder into `~/.claude/skills/`.

## Links

- Website: [repping.ai](https://www.repping.ai)
- MCP docs: [repping.ai/mcp](https://www.repping.ai/mcp)
- Free creator guides and tools: [learn.repping.ai](https://learn.repping.ai)
- Support: support@repping.ai
- Privacy: [repping.ai/privacy](https://www.repping.ai/privacy)

## License

MIT © Repping Labs LLC
