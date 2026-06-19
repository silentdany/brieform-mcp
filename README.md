# Brieform MCP Server

### Build forms inside your AI chat.

[![View on Glama](https://img.shields.io/badge/View%20on-Glama-060f11)](https://glama.ai/mcp/connectors/app.brieform/brieform)
[![Website](https://img.shields.io/badge/Website-brieform.app-2563eb)](https://brieform.app)
[![MCP](https://img.shields.io/badge/MCP-streamable--http-555)](https://modelcontextprotocol.io)

**AI-native form builder with a native MCP server: create, publish, and read form responses from Claude, ChatGPT, Cursor, and any MCP client. No dashboard, no second tab.**

> ℹ️ **This repository is docs only.** Brieform is a hosted service. The server runs at `https://brieform.app/api/mcp/mcp` and there's nothing to install or build here. This repo holds the connection guide, manifest, and client examples. Issues and feature requests are welcome.

---

## Why Brieform

Most form builders bolt an MCP server onto a dashboard designed for clicking. Brieform is conversation-first. When you live in Claude or Cursor, building a form still forces a context switch: open a second tool, re-enter every field, collect responses, paste them back into chat. Your AI does the thinking; you do the switching.

Brieform closes that loop: connect once, describe a form, get a live URL back, and read every response in the same thread.

## How it works

1. **Connect once.** Add Brieform's MCP URL in your client's MCP settings.
2. **Describe a form.** *"Create a contact form with name, email, and a message field."* You get a live URL back.
3. **Read responses in the same thread.** `get_responses` returns them in the conversation. No dashboard.

```
You:    Create a customer feedback form: rating /5, what we can improve, optional email. Make it green.
Claude: Done. Live at https://brieform.app/f/your-form (preview rendered in chat)
You:    Any responses yet?
Claude: 4 responses. Average rating 4.25/5. Top theme: faster support replies.
```

## Connect

Brieform is a **remote (hosted) MCP server** over streamable HTTP, with OAuth. Add it to your MCP client's config:

```json
{
  "mcpServers": {
    "brieform": {
      "type": "streamable-http",
      "url": "https://brieform.app/api/mcp/mcp"
    }
  }
}
```

On first use, your client opens an OAuth login to connect your Brieform account, with no API key to manage. Sign up free at [brieform.app](https://brieform.app).

Client-specific configs are in [`examples/`](./examples). You can also [try it in your browser](https://glama.ai/mcp/inspector?servers=%5B%7B%22authType%22%3A%22oauth%22%2C%22id%22%3A%22https%3A%2F%2Fbrieform.app%2Fapi%2Fmcp%2Fmcp%22%2C%22name%22%3A%22Brieform%22%2C%22url%22%3A%22https%3A%2F%2Fbrieform.app%2Fapi%2Fmcp%2Fmcp%22%7D%5D) via the Glama Inspector.

## The 12 MCP tools

Full form lifecycle, all from chat:

| Tool | What it does |
|------|--------------|
| `create_form` | Generate a form from a natural-language description (or structured fields) |
| `update_form` | Edit fields, layout, logic, or copy |
| `publish_form` | Make a draft public and get its live URL |
| `unpublish_form` | Take a form offline (responses preserved) |
| `get_form` | Fetch a form's full structure |
| `list_forms` | List your forms with status and response counts |
| `duplicate_form` | Clone an existing form |
| `delete_form` | Remove a form (requires explicit confirmation) |
| `set_form_theme` | Apply a theme (8 presets or custom colors) |
| `get_responses` | Read submissions in the conversation (CSV export for large sets) |
| `get_form_analytics` | Views, submissions, conversion rate, referrers, funnel |
| `get_form_share_assets` | Public URL, embed snippet, social image, QR code |

## Features

- **13 field types**: text, email, tel, textarea, select, radio, checkbox, rating, date, number, url, password, GDPR consent
- **Multi-step forms** with progress bar
- **Conditional logic**: 8 operators for show/hide and branching
- **8 theme presets** plus custom theming
- **GDPR consent** built in, **EU hosting** (Frankfurt)
- **Spam protection** out of the box
- **CSV export** on every plan
- **Live preview widget** rendered directly in compatible chat clients (Claude)
- **Audit log**: every MCP write operation recorded in the form's Activity tab

## Compatibility

Works with any MCP client, including **Claude**, **ChatGPT**, **Cursor**, **Le Chat (Mistral)**, **Perplexity**, and **VS Code + GitHub Copilot**.

## Pricing

| Plan | Monthly | Key limits |
|------|---------|------------|
| **Free** | $0 | 1 active form, 50 responses/mo, 11/12 MCP tools, no credit card |
| **Starter** | $29/mo | 20 forms, 2,000 responses, all 12 tools (analytics included), branding removed |
| **Pro** | $69/mo | Unlimited forms & responses, all 12 tools, priority support |

> **Founders Rate:** 50% off for life on Starter and Pro, for the first 30 customers, applied automatically.

## Links

- Website & sign-up: https://brieform.app
- Glama connector: https://glama.ai/mcp/connectors/app.brieform/brieform
- Official MCP registry: `app.brieform/brieform`

## Support

Found a bug or have a feature request? [Open an issue](../../issues). For account or billing questions, see [brieform.app](https://brieform.app).

---

Built by [Dany](https://x.com/MajorBaguette) · Made for teams who already live in their chat client.
