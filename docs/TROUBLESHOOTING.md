# 🛠️ Troubleshooting Guide

Use this guide to quickly diagnose and fix common Ops Intake Copilot issues.

---

## 🤖 Bot Not Responding

### Symptoms

- No reply in Discord after posting a message.
- n8n workflow does not trigger.

### Checks

1. Verify workflow is **Active** in n8n.
2. Confirm bot is online in Discord member list.
3. Ensure bot has channel permissions:
   - View channel
   - Read message history
   - Send messages
4. Confirm `MESSAGE CONTENT INTENT` is enabled in Discord Developer Portal.
5. Check n8n execution logs for trigger errors.

### Fixes

- Re-invite bot with correct OAuth scopes/permissions.
- Re-save credentials in n8n.
- Restart n8n and bot service if self-hosted.

---

## 🔁 Bot Reading Its Own Messages (Loop)

### Symptoms

- Bot repeatedly responds to itself.
- Rapid duplicate replies/issues.

### Checks

1. Verify filter logic ignores messages where `author.bot == true`.
2. Confirm responder bot and trigger bot are handled separately.
3. Ensure webhook node only handles user messages.

### Fixes

- Add early guard clause in workflow:

```json
{
  "if": "message.author.bot === true",
  "action": "stop"
}
```

- Use a dedicated intake channel where only humans post bug reports.

---

## 🐙 GitHub Issues Not Creating

### Symptoms

- Discord says issue creation failed.
- n8n run reaches GitHub node with error.

### Checks

1. Validate GitHub token is not expired/revoked.
2. Confirm token has **Issues write** permissions.
3. Verify repository owner/name is correct.
4. Check repository allows issues.

### Fixes

- Regenerate token and update n8n credential.
- Test token manually using API:

```bash
curl -H "Authorization: Bearer $GITHUB_TOKEN" https://api.github.com/user
```

- Confirm issue creation endpoint payload fields are valid.

---

## 🧠 AI Not Extracting Properly

### Symptoms

- Missing fields in parsed output.
- Misclassification of reports.

### Checks

1. Verify Groq API key is valid.
2. Confirm model name is correct (e.g., LLaMA 3 variant).
3. Inspect prompt instructions in n8n for deterministic field extraction.
4. Check malformed JSON parsing in response handling.

### Fixes

- Tighten prompt format with explicit schema output.
- Add fallback defaults for missing optional fields.
- Add validation step before GitHub node.

---

## ♻️ Duplicate Issues

### Symptoms

- Same report creates multiple GitHub issues.

### Checks

1. Confirm webhook retries are handled idempotently.
2. Check if multiple workflows listen to same channel/webhook.
3. Verify user message ID dedupe logic exists.

### Fixes

- Store processed Discord message IDs (KV/DB/cache).
- Skip creation when `message_id` already processed.
- Add delay + lock pattern for high traffic channels.

---

## 🌐 Webhook / Cloudflare Tunnel Issues

### Symptoms

- Discord cannot reach webhook.
- n8n URL works locally but not externally.

### Checks

1. Confirm tunnel is running.
2. Verify `WEBHOOK_URL` matches current public URL.
3. Ensure HTTPS URL is used (not HTTP).
4. Check Cloudflare tunnel logs for connection errors.

### Fixes

- Restart tunnel:

```bash
cloudflared tunnel --url http://localhost:5678
```

- Update n8n webhook base URL and reactivate workflow.
- Avoid rotating URLs by using named persistent tunnels.

---

## ⚡ Quick Reference

| Problem | Most Likely Cause | Fastest Fix |
| --- | --- | --- |
| Bot silent | Missing intents or permissions | Enable intents + re-invite bot |
| Message loop | Bot messages not filtered | Ignore `author.bot == true` |
| No GitHub issue | Token/repo permission issue | Regenerate token with issues write |
| Bad AI extraction | Prompt or parsing mismatch | Enforce strict JSON schema output |
| Duplicates | No dedupe/idempotency | Track Discord message IDs |
| Webhook offline | Tunnel/URL mismatch | Restart tunnel + update `WEBHOOK_URL` |

---

If issues persist, collect:

- n8n execution ID
- Relevant node error output
- Sample Discord input
- API response snippets (with secrets redacted)

Then open a bug report with this diagnostic data.
