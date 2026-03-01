# 🤖 Ops Intake Copilot

[![n8n](https://img.shields.io/badge/n8n-v2.9.4-blue)](https://n8n.io)
[![Groq](https://img.shields.io/badge/Groq-LLaMA%203-green)](https://groq.com)
[![Discord](https://img.shields.io/badge/Discord-Bot-purple)](https://discord.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Zero-cost automated bug intake from Discord to GitHub Issues using AI**

![Demo](images/demo.gif)

## ✨ Features
- 🤖 **AI-Powered Extraction** - Uses Groq LLaMA 3 to parse bug reports
- 📋 **Smart Routing** - Asks for missing information automatically
- 🐙 **GitHub Integration** - Creates formatted issues with labels
- 💰 **100% Free** - Only uses generous free tiers
- 🚀 **Self-Hosted** - Runs on your own infrastructure

## 🛠️ Architecture
![Architecture Diagram](images/architecture.png)

1. User types bug report in Discord
2. n8n Trigger Bot forwards to webhook
3. n8n workflow processes with Groq AI
4. Complete reports → GitHub Issues
5. Incomplete reports → Bot asks for details

## 📦 Tech Stack
- **n8n** - Workflow automation (self-hosted)
- **Groq API** - AI processing (free tier)
- **Discord** - Chat interface
- **GitHub Issues** - Ticket tracking
- **Cloudflare** - Tunnel for webhooks

## 🚀 Quick Start
[Installation instructions here...]

## 📊 Example
