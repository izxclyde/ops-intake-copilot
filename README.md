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
