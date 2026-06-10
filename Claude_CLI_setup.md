# Claude Code + Qwen Setup Guide (Windows)
### Use Claude Code CLI with Qwen Paid Models — No Anthropic Account Needed!

---

## Table of Contents
1. [What is This?](#what-is-this)
2. [Requirements](#requirements)
3. [Step 1: Install Node.js](#step-1-install-nodejs)
4. [Step 2: Install Qwen CLI](#step-2-install-qwen-cli)
5. [Step 3: Install Claude Code + Router](#step-3-install-claude-code--router)
6. [Step 4: Get Your Qwen API Key](#step-4-get-your-qwen-api-key)
7. [Step 5: Create Config File](#step-5-create-config-file)
8. [Step 6: Start Claude Code](#step-6-start-claude-code)
9. [Troubleshooting](#troubleshooting)
10. [Quick Reference](#quick-reference)

---

## What is This?

This guide helps you use **Claude Code** (Anthropic's powerful AI coding assistant) using your **Qwen paid API key** — without needing an Anthropic account.

| Tool | Purpose |
|---|---|
| **Claude Code** | The AI coding assistant (interface) |
| **Claude Code Router (CCR)** | Connects Claude Code to Qwen models |
| **Qwen API** | Powers Claude Code with Qwen3 Coder Plus model |

> **No Anthropic account needed. Just your Qwen API key.**

---

## Requirements

| Requirement | Details |
|---|---|
| Operating System | Windows 10 or Windows 11 |
| Node.js | v18 or later |
| Qwen API Key | From Alibaba Cloud (paid plan) |

---

## Step 1: Install Node.js

1. Go to [nodejs.org](https://nodejs.org)
2. Click **Download Node.js (LTS)** — the LTS version is recommended
3. Run the downloaded installer (`node-vxx.x.x-x64.msi`) and follow the prompts
4. Make sure **"Add to PATH"** is checked during installation

![Node.js download page](images/step1-node-download.png)

![Node.js installer](images/step1-node-installer.png)

**Verify installation** — open Command Prompt and run:

```
node --version
npm --version
```

![Node.js version check](images/step1-node-version.png)

You should see `v20.x.x` for Node.js and `10.x.x` (or higher) for npm.

---

## Step 2: Install Qwen CLI

Open **Command Prompt** and run:

```
npm install -g @qwen-code/qwen-code@latest
```

![Installing Qwen CLI](images/cli-step2-qwen-install.png)

**Verify installation:**

```
qwen --version
```

![Qwen CLI version check](images/cli-step2-qwen-version.png)

You should see a version number like `0.15.6`.

---
