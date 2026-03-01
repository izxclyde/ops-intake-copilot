# ⚙️ Ops Intake Copilot Setup Guide

This guide walks you through a full setup of Ops Intake Copilot with:

- n8n (self-hosted)
- Groq API
- Discord bots
- GitHub Issues
- Cloudflare Tunnel

---

## ✅ Prerequisites

Before starting, make sure you have:

- A running self-hosted **n8n** instance
- A **GitHub** account with access to target repository issues
- A **Groq** account for API access
- A **Discord** server with permission to add/manage bots
- **Cloudflare Tunnel** installed (or similar public tunnel)

Optional but recommended:

- A dedicated Discord channel like `#bug-reports`
- A separate GitHub label set (e.g., `bug`, `triage`, `discord-intake`)

---

## 1) Create GitHub Token (Issues Write Access)

1. Go to GitHub: **Settings → Developer Settings → Personal access tokens**.
2. Choose either:
   - Fine-grained token (recommended), or
   - Classic token (`repo` scope).
3. Grant access to the target repository.
4. Ensure permissions include **Issues: Read and write**.
5. Copy token and store it securely.

Example secret storage:

```bash
export GITHUB_TOKEN=ghp_xxxxxxxxxxxxxxxxxxxxx
```

---

## 2) Create Groq API Key

1. Sign in to [Groq Console](https://console.groq.com/).
2. Open **API Keys**.
3. Create a new key.
4. Copy and securely store the key.

```bash
export GROQ_API_KEY=gsk_xxxxxxxxxxxxxxxxxxxxx
```

---

## 3) Create Discord Bots

You need **two bot roles** in this architecture:

- **A. n8n Trigger Bot** (receives channel events/messages)
- **B. Custom Bot** (posts friendly responses/requests for details)

> You can implement both behaviors with one bot token if your workflow supports it, but separating responsibilities is cleaner for maintenance.

### A) n8n Trigger Bot Setup

1. Go to [Discord Developer Portal](https://discord.com/developers/applications).
2. Create a new application (e.g., `Ops Intake Trigger`).
3. In **Bot** tab, create bot and copy token.
4. Enable intents needed for your workflow:
   - `MESSAGE CONTENT INTENT`
   - `SERVER MEMBERS INTENT` (only if required)
5. Under OAuth2 URL Generator:
   - Scopes: `bot`
   - Bot permissions: `Read Messages/View Channels`, `Send Messages`, `Read Message History`
6. Invite bot to your server.

```bash
export DISCORD_TRIGGER_BOT_TOKEN=xxxxxxxxxxxxxxxxxxxxx
```

### B) Custom Response Bot Setup

1. Create a second Discord application (e.g., `Ops Intake Responder`).
2. Create bot and copy token.
3. Grant permissions:
   - `Send Messages`
   - `Embed Links`
   - `Read Message History`
4. Invite to same server/channel.

```bash
export DISCORD_RESPONSE_BOT_TOKEN=xxxxxxxxxxxxxxxxxxxxx
```

---

## 4) Configure n8n Credentials

In n8n UI, create credentials for:

- **GitHub API** credential
  - Token: `GITHUB_TOKEN`
- **HTTP Header Auth** or generic API credential for Groq
  - Header: `Authorization: Bearer <GROQ_API_KEY>`
- **Discord credentials**
  - Trigger bot token
  - Response bot token (if separate)

Recommended environment variables for n8n deployment:

```bash
N8N_HOST=localhost
N8N_PORT=5678
N8N_PROTOCOL=http
WEBHOOK_URL=https://your-public-url.example.com/
```

---

## 5) Configure Cloudflare Tunnel (Webhook Access)

If n8n is local/private, expose it publicly so Discord webhooks can reach it.

```bash
cloudflared tunnel login
cloudflared tunnel create ops-intake-copilot
cloudflared tunnel --url http://localhost:5678
```

Copy the generated HTTPS URL and set it in n8n as `WEBHOOK_URL`.

---

## 6) Import and Configure n8n Workflow

1. Open n8n.
2. Go to **Workflows → Import from File**.
3. Import your Ops Intake Copilot workflow JSON.
4. Open each node and map credentials:
   - Discord Trigger
   - Groq API request
   - Classification logic (complete/incomplete/question)
   - GitHub Issue creation
   - Discord response node
5. Save and activate workflow.

---

## 7) Webhook Configuration Checklist

- n8n workflow is **Active**.
- Webhook URL is public and HTTPS.
- Discord bot has channel access.
- Bot intents include message content.
- GitHub token can write issues.
- Groq key is valid and not rate-limited.

---

## 8) Testing Instructions

### Test A: Complete bug report

Send in Discord:

```text
Search page crashes after pressing Enter.
Device: Pixel 7
Browser: Chrome 125
Steps: Open search -> type term -> press Enter
Expected: results page loads
Actual: app freezes and reloads
Severity: High
```

Expected result:

- Workflow classifies as complete.
- GitHub Issue is created.
- Discord reply includes issue URL.

### Test B: Incomplete report

```text
Export does not work.
```

Expected result:

- Workflow asks for missing details.
- No issue created yet.

### Test C: Question/greeting

```text
Hi bot, how do I file a good bug report?
```

Expected result:

- Workflow sends guidance response.
- No issue created.

---

## ✅ Setup Complete

Once these tests pass, your Ops Intake Copilot is live and ready to triage bug reports automatically from Discord to GitHub.
