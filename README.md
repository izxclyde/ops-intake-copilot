# 🤖 Ops Intake Copilot

[![n8n](https://img.shields.io/badge/n8n-v2.9.4-blue)](https://n8n.io)
[![Groq](https://img.shields.io/badge/Groq-LLaMA%203-green)](https://groq.com)
[![Discord](https://img.shields.io/badge/Discord-Bot-purple)](https://discord.com)
[![GitHub](https://img.shields.io/badge/GitHub-Issues-black)](https://github.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Cost](https://img.shields.io/badge/Cost-%240-brightgreen)](https://github.com)

**Zero-cost automated bug intake from Discord to GitHub Issues using AI**

## 📋 Table of Contents
- [Features](#-features)
- [How It Works](#-how-it-works)
- [Tech Stack](#-tech-stack)
- [Quick Start](#-quick-start)
- [Cost Breakdown](#-cost-breakdown)
- [Examples](#-examples)
- [Documentation](#-documentation)
- [License](#-license)

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🤖 **AI-Powered Extraction** | Uses Groq LLaMA 3 to parse unstructured bug reports |
| 📋 **Smart Routing** | Detects questions vs. bugs, asks for missing info |
| 🐙 **GitHub Integration** | Creates formatted issues with labels and templates |
| 💰 **100% Free** | Only uses generous free tiers from all platforms |
| 🚀 **Self-Hosted** | Runs on your own n8n instance with Cloudflare tunnel |
| 🔄 **Real-time** | Instant processing with Discord webhooks |

## 🔄 How It Works

```mermaid
graph LR
    A[Discord User] -->|Bug Report| B[n8n Trigger Bot]
    B -->|Webhook| C[n8n Workflow]
    C -->|AI Analysis| D[Groq LLaMA 3]
    C -->|Complete Report| E[GitHub Issues]
    C -->|Missing Info| F[Custom Discord Bot]
    F -->|Ask for details| A
    E -->|Issue URL| F
🛠️ Tech Stack
Component	Technology	Cost
Automation Engine	n8n (self-hosted)	$0
AI Processing	Groq (LLaMA 3)	$0
Chat Interface	Discord + n8n Trigger Bot	$0
Issue Tracking	GitHub Issues	$0
Tunneling	Cloudflare Tunnel	$0
Response Bot	Custom Discord Bot	$0
TOTAL		$0
🚀 Quick Start
Prerequisites
n8n self-hosted instance (v2.9.4+)

Cloudflare tunnel (or ngrok)

Discord server with "Manage Server" permissions

GitHub account

5-Minute Setup
Clone this repository

bash
git clone https://github.com/yourusername/ops-intake-copilot.git
cd ops-intake-copilot
Import the n8n workflow

Open your n8n instance

Go to Workflows → Import from File

Select workflow/ops-intake-copilot.json

Set up Discord bots

Invite n8n Trigger Bot: https://discord.com/discovery/applications/1389933424331980993

Create Custom Bot (see SETUP.md)

Configure credentials in n8n

GitHub Personal Access Token

Groq API Key

Discord Bot Token

Activate the workflow

Toggle the workflow to Active

Test with: App crashes on iPhone with Safari

📚 For detailed instructions, see SETUP.md

💰 Cost Breakdown
Service	Tier Used	Limits	Cost
n8n	Self-hosted	Unlimited	$0
Cloudflare	Free	Unlimited tunnels	$0
Discord	Free	Unlimited messages	$0
Groq	Free	500K tokens/minute	$0
GitHub	Free	Unlimited repos	$0
Monthly Total			$0
📝 Examples
Input: Complete Bug Report
text
App crashes when I try to upload a profile picture. 
Using iPhone 14 Pro with Safari. 
Click upload button, app closes immediately. 
This is critical!
Output: Discord Response
text
🔴 **Bug Report Created!**

**Title:** App crashes during upload
**Device:** iPhone 14 Pro
**Browser:** Safari
**Severity:** High

🔗 **GitHub Issue:** https://github.com/user/repo/issues/42
📚 Documentation
Setup Guide - Complete installation instructions

Architecture - System design and data flow

Troubleshooting - Common issues and solutions

Examples - Test messages and sample outputs

📄 License
This project is licensed under the MIT License - see the LICENSE file.

<p align="center"> Built with ❤️ for the developer community <br> <a href="https://github.com/yourusername/ops-intake-copilot">⭐ Star on GitHub</a> </p> ```
