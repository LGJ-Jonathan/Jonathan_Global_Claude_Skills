---
name: multi-agent-ops
description: Patterns and operational guide for multi-agent coordination in OpenAgents workspaces. Covers agent discovery, task delegation, shared vs local resources, cross-agent communication, and the capability matrix across agents. Use when planning multi-agent workflows, delegating tasks, or understanding what each agent can access. Triggers on mentions of multi-agent, agent coordination, agent capabilities, task delegation, or workspace orchestration.
---

# Multi-Agent Operations

## When to use this skill
- Planning work across multiple agents
- Understanding which agent should handle which task
- Delegating tasks to other agents
- Debugging cross-agent communication issues
- Setting up new agents in a workspace

## Agent Architecture

### Shared resources (via MCP — all agents)
- **BridgeKit**: Google Docs, Sheets, Gmail, Slack, Bison, Instantly
- **Playwright**: Full browser automation
- **OpenAgents Workspace**: Shared browser, workspace files, tunnels, chat
- **Workspace chat**: Primary coordination channel

### Local resources (per-agent, NOT shared)
- **Filesystem**: Each agent has its own machine and home directory
- **CLI tools**: `gh`, `node`, `python`, etc. — depends on local install
- **API tokens**: Railway token, GitHub auth — stored in local env
- **Git repos**: Cloned locally per agent

## Agent Discovery

### Check who's online
```
workspace_get_agents -> lists all connected agents with status
```

### Communicate with agents
- **@mention** an agent in your text response to send them work
- Only @mention when you need them to **do something**
- Do NOT @mention just to say thanks or acknowledge

## Capability Matrix

| Capability | Shared (MCP) | Local (per-agent) |
|-----------|-------------|-------------------|
| Google Workspace (Docs/Sheets/Gmail) | Yes | - |
| Slack messaging | Yes | - |
| Bison/Instantly campaign mgmt | Yes | - |
| Browser automation (Playwright) | Yes | - |
| Shared browser (workspace) | Yes | - |
| Cloudflare tunnels | Yes | - |
| Workspace file storage | Yes | - |
| GitHub CLI (`gh`) | - | Needs local install |
| Railway deploy | - | Needs local token |
| Local file system | - | Agent-specific |
| Git operations | - | Agent-specific |
| Package managers (npm, pip, brew) | - | Agent-specific |

## Task Delegation Patterns

### By capability
- **Google Workspace tasks** -> Any agent (shared MCP)
- **Code writing/editing** -> Agent with repo cloned locally
- **GitHub repo creation** -> Agent with `gh` CLI installed + authenticated
- **Railway deployment** -> Agent with Railway token
- **Browser testing** -> Any agent (Playwright is shared)
- **Cold email ops** -> Any agent (BridgeKit is shared)

### By workload
- Use `superpowers:dispatching-parallel-agents` for 2+ independent tasks
- Each agent can work on its own task simultaneously
- Coordinate via workspace chat — share results as workspace files

### Handoff pattern
```
1. Agent A finishes code -> pushes to GitHub
2. Agent A @mentions Agent B: "Code pushed to repo X, deploy to Railway"
3. Agent B pulls code -> runs Railway deploy pipeline
4. Agent B reports back in workspace chat
```

## Cross-Agent Data Exchange

### Via workspace files (recommended)
```
Agent A: workspace_write_file("report.json", data)
Agent B: workspace_read_file("report.json")
```

### Via workspace chat
```
Agent A: Posts results as text in chat response
Agent B: workspace_get_history() to read
```

### Via shared services
```
Agent A: Writes to Google Sheet via BridgeKit
Agent B: Reads from same Google Sheet via BridgeKit
```

## Setting Up a New Agent

### Minimum setup for full capability
1. Install `gh` CLI + authenticate: `gh auth login`
2. Set Railway token: `export RAILWAY_TOKEN=...` in shell profile
3. Clone needed repos locally
4. Verify MCP tools available: `ToolSearch` for BiridgeKit, playwright, openagents-workspace

### Verify agent environment
```bash
# Check local tools
which gh node npm python3
gh auth status
echo $RAILWAY_TOKEN

# Check OS
uname -s -m
echo $HOME
hostname
```

## Important Notes
- Agents on different machines do NOT share filesystems
- MCP tools are the universal bridge — always available to all agents
- Use workspace_get_agents to verify who's online before delegating
- Keep @mentions purposeful — each one wakes the target agent
- Workspace chat messages persist and can be read by any agent via history
