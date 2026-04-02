---
name: openagents-workspace
description: OpenAgents workspace MCP tools for multi-agent collaboration, shared browser control, file management, Cloudflare tunnels, and workspace chat. Use when coordinating between agents, sharing browser sessions, exposing local ports, or managing workspace files. Triggers on mentions of workspace, agents, tunnels, shared browser, or multi-agent coordination.
---

# OpenAgents Workspace MCP Integration

## When to use this skill
- Coordinating work between multiple agents in a workspace
- Controlling a shared browser (navigate, click, type, screenshot)
- Exposing local dev servers via Cloudflare tunnels
- Reading/writing files to the shared workspace filesystem
- Checking workspace status or agent availability
- Reading workspace chat history

## How to access tools
All tools are prefixed with `mcp__openagents-workspace__`. Use `ToolSearch` with query `"+openagents-workspace"` to fetch schemas.

## Tool Inventory

### Agent & Workspace Management

| Tool | Purpose |
|------|---------|
| `workspace_get_agents` | List all connected agents with status |
| `workspace_get_history` | Read workspace chat history |
| `workspace_status` | Get workspace connection status |

### Shared Browser Control

| Tool | Purpose |
|------|---------|
| `workspace_browser_open` | Open a new browser tab |
| `workspace_browser_close` | Close a browser tab |
| `workspace_browser_navigate` | Navigate to a URL |
| `workspace_browser_click` | Click element by CSS selector |
| `workspace_browser_type` | Type text into an element |
| `workspace_browser_screenshot` | Take screenshot of current page |
| `workspace_browser_snapshot` | Get DOM snapshot |
| `workspace_browser_list_tabs` | List all open tabs |
| `workspace_browser_list_contexts` | List browser contexts |

### Cloudflare Tunnels

| Tool | Purpose |
|------|---------|
| `tunnel_expose` | Expose a local port as a public URL |
| `tunnel_close` | Close an active tunnel |
| `tunnel_list` | List all active tunnels |

### Workspace File Management

| Tool | Purpose |
|------|---------|
| `workspace_read_file` | Read a file from workspace storage |
| `workspace_write_file` | Write a file to workspace storage |
| `workspace_delete_file` | Delete a file from workspace storage |
| `workspace_list_files` | List files in workspace storage |

## Common Patterns

### Multi-agent coordination
1. Check who's online: `workspace_get_agents`
2. Read recent context: `workspace_get_history`
3. @mention agents in chat to delegate work
4. Share files via `workspace_write_file` for other agents to read

### Exposing a dev server
```
1. Start your dev server locally (e.g., port 3000)
2. tunnel_expose(port=3000) -> returns public URL
3. Share the URL with the team or use for testing
4. tunnel_close(port=3000) when done
```

### Shared browser testing
```
1. workspace_browser_open() -> get tab_id
2. workspace_browser_navigate(tab_id, url)
3. workspace_browser_screenshot(tab_id) -> verify state
4. workspace_browser_click(tab_id, selector)
5. workspace_browser_type(tab_id, selector, text)
6. workspace_browser_close(tab_id)
```

### Workspace files vs local files
- **Workspace files** (`workspace_read_file`/`workspace_write_file`): Shared across all agents in the workspace. Use for cross-agent data exchange.
- **Local files** (`Read`/`Write`): Only on the local machine. Not shared with other agents on different machines.

## Agent Communication
- To message another agent: @mention them in your text response
- Only @mention agents when you need them to do work
- Agents on different machines do NOT share local filesystems
- Agents DO share: MCP tools (BridgeKit, Playwright, workspace tools), workspace chat, workspace files

## Important Notes
- Browser operations require a `tab_id` from `workspace_browser_open` or `workspace_browser_list_tabs`
- CSS selectors are used for `workspace_browser_click` and `workspace_browser_type`
- Tunnels use Cloudflare — URLs are public but temporary
- Workspace chat is the primary coordination mechanism between agents
