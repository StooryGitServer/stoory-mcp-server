# Stoory MCP Server

**Hire a human specialist from your AI workspace — without leaving Claude Code.**

AI can build most of your app. It can't get you GDPR-compliant, review your
Stripe integration, design your landing page, or run your SEO. Stoory MCP lets
your AI coding assistant find, brief, and hire the right human for that —
without you ever opening Upwork, writing a job post, or explaining your
problem from scratch.

---

## What it does

- **Search** Stoory's marketplace (400+ specializations: dev, legal, design,
  growth, operations) with a natural-language query.
- **Package a task**: your AI assistant drafts the title, description, and
  budget, and picks only the files the specialist actually needs — never your
  whole repo.
- **Hand off safely**: a private GitHub repo is created per task, shared only
  with the invited specialist.
- **Track progress**: check status and pull results back into your AI
  workspace once the specialist is done.

You stay in control of the two decisions that matter — **who to hire** and
**what budget to approve**. The agent does the rest.

See [Tools](#tools) below for the full list.

---

## Quickstart

### Requirements

- An AI client that supports MCP over Streamable HTTP (Claude Code, Claude
  Desktop, Cursor, ...).
- A free Stoory client account and API key (below).

### 1. Get a client API key

Sign up at
[stoory.io/login?step=register&u=Client_(user)](https://stoory.io/login?step=register&u=Client_\(user\)),
then open **MCP Server** on the Stoory homepage to generate your
`client_api_key`.

### 2. Add the server to your AI client

```json
{
  "mcpServers": {
    "stoory": {
      "url": "https://mcp.stoory.io/mcp",
      "headers": {
        "x-client-api-key": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

Claude Code CLI:

```bash
claude mcp add --transport http stoory \
  https://mcp.stoory.io/mcp \
  --header "x-client-api-key: YOUR_API_KEY_HERE"
```

### 3. Ask for help

> "Claude keeps breaking my Stripe integration. Find me someone who can fix it."

That's it — the assistant searches, drafts the task, shows you cost and
files before anything is sent, and waits for your go-ahead.

---

## Tools

| Tool | What it does |
|---|---|
| `search_specialists` | Semantic search over Stoory's specialist marketplace |
| `create_task` | Drafts and sends a task to one or more chosen specialists (requires explicit user confirmation) |
| `get_task_status` | Checks whether a specialist has accepted / is working / has finished |
| `get_task_result` | Returns the link to the task's private result repo |
| `get_task_repo_files` | Reads the result files directly, so the assistant can review the work itself |
| `cancel_task` | Cancels a task before a specialist has accepted it |

---

## How it works

```
"I need a GDPR specialist"
        │
        ▼
AI searches the marketplace, you pick a specialist
        │
        ▼
AI drafts the task + selects only the needed files
        │
        ▼
You confirm cost and file list
        │
        ▼
Private GitHub workspace created, specialist invited
        │
        ▼
You pull the result back into your AI workspace
```

---

## Security & privacy

**Your private data doesn't need to become public just because you need
human help.**

- Your assistant chooses which files to share — never the whole repo.
- Every task with attachments gets its own **private** GitHub repo, visible
  only to the invited specialist.
- Files are scanned for secrets (`.env`, private keys, API keys/tokens)
  before anything leaves your machine.
- Nothing is shared, and no task is created, without your explicit
  confirmation.

---

## Example

```
User: "I've built my SaaS with Claude Code. I need a privacy policy
       and terms of service before I can launch."

Claude: 5 relevant specialists found.

User: "Use #2, budget $200."

Claude: Creates the task, writes the brief, selects the relevant
        project files, opens a private repo, and shares it with
        the specialist. Done.
```

---

## Community & support

- Marketplace & signup: [stoory.io](https://stoory.io)
- Issues / bugs: [GitHub Issues](https://github.com/StooryGitServer/stoory-mcp-server/issues)
- MCP Registry entry: `io.github.stoorygitserver/stoory-mcp`

---

## Disclaimer

Stoory MCP does not replace your AI assistant and does not perform payments
or hiring decisions on its own — it prepares the task and hands the decision
to you. Payment between client and specialist happens outside this system,
directly through Stoory.
```
