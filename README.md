# LeafPad Claude Code plugin

LeafPad is a blogging/CMS product by **Bokimo Technologies LLP**. This plugin connects Claude Code to the LeafPad remote MCP server at `https://leafpad.io/mcp` (OAuth via Scalekit) and adds skills for writing posts and scheduling content refreshes.

## What you get

- **Remote MCP server** `leafpad` → `https://leafpad.io/mcp`
- **Skill** `write-and-publish-post` — draft, SEO-check, and publish with consent
- **Skill** `schedule-rewrites` — find decaying pages, review proposals, schedule AI rewrites

You need a LeafPad account. Sign up at [leafpad.io](https://leafpad.io).

## Install from a marketplace (recommended)

Host this folder in a **public GitHub repository** (plugin at the repo root, with `.claude-plugin/marketplace.json` present). Then in Claude Code:

```bash
# Add the marketplace once (replace with your GitHub owner/repo)
claude plugin marketplace add YOUR_ORG/leafpad-claude-plugin

# Install the plugin
claude plugin install leafpad@leafpad-marketplace
```

Inside a session you can also use:

```text
/plugin marketplace add YOUR_ORG/leafpad-claude-plugin
/plugin install leafpad@leafpad-marketplace
```

Or the one-shot form (Claude Code v2.1.275+ in-session / v2.1.292+ from the shell):

```bash
claude plugin install leafpad --marketplace YOUR_ORG/leafpad-claude-plugin
```

## Load without a marketplace

```bash
# Directory
claude --plugin-dir /path/to/leafpad-claude-plugin

# Or a zip of this folder
claude --plugin-dir /path/to/leafpad-claude-plugin.zip
```

## Authenticate

After install, open `/mcp` in Claude Code and complete the LeafPad OAuth sign-in when the `leafpad` server shows as needing authentication.

## Docs

- MCP setup guide: https://leafpad.io/docs/ai/Leafpad-blog-mcp
- Privacy: https://leafpad.io/privacy
- Support: support@leafpad.io · https://leafpad.io/contact

## License

MIT — see [LICENSE](./LICENSE).
