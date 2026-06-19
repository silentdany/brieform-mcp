# Connecting Brieform to your MCP client

Brieform is a **remote streamable-HTTP** MCP server with OAuth. The endpoint is:

```
https://brieform.app/api/mcp/mcp
```

On first connection, your client opens a browser OAuth login to link your Brieform account. No API key required.

Pick the config that matches your client below. Exact config locations and field names can vary by client version, so when in doubt, see the connection guide at [brieform.app](https://brieform.app).

| Client | File | Example |
|--------|------|---------|
| Claude Desktop | `claude_desktop_config.json` | [`claude-desktop.json`](./claude-desktop.json) |
| Cursor | `~/.cursor/mcp.json` | [`cursor.json`](./cursor.json) |
| VS Code (Copilot) | `.vscode/mcp.json` | [`vscode-mcp.json`](./vscode-mcp.json) |

### Try it without installing

Open the [Glama Inspector with Brieform preloaded](https://glama.ai/mcp/inspector?servers=%5B%7B%22authType%22%3A%22oauth%22%2C%22id%22%3A%22https%3A%2F%2Fbrieform.app%2Fapi%2Fmcp%2Fmcp%22%2C%22name%22%3A%22Brieform%22%2C%22url%22%3A%22https%3A%2F%2Fbrieform.app%2Fapi%2Fmcp%2Fmcp%22%7D%5D) and exercise the 12 tools in your browser.

### Clients that only support stdio

Some older clients don't speak remote HTTP directly. Bridge with [`mcp-remote`](https://www.npmjs.com/package/mcp-remote):

```json
{
  "mcpServers": {
    "brieform": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://brieform.app/api/mcp/mcp"]
    }
  }
}
```
