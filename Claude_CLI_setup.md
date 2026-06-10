
# Claude CLI Setup Guide
### How to Use Claude Code CLI with Claude Code Router (CCR) + Qwen

---

## Prerequisites

Before getting started, make sure you have the following:

- Windows 10/11 or WSL (Windows Subsystem for Linux)
- **Node.js** installed — download from [nodejs.org](https://nodejs.org)
- **CCR configured with Qwen** — complete Steps 1–5 from the [Cowork setup guide](Claude_Cowork_setup.md) first
- Internet connection

---
 
## Step 1 — Install Claude Code CLI

Run the following command in your terminal:

```
npm install -g @anthropic-ai/claude-code
```

![Installing Claude Code CLI via npm](images/cli-step1-install.png)

After installation, verify it works:

```
claude --version
```

![Claude CLI version check](images/cli-step1-version.png)

---
 
## Step 2 — Get Your Qwen API Key

1. Go to: [modelstudio.console.alibabacloud.com](https://modelstudio.console.alibabacloud.com)
2. Create an account (select the **Singapore** region)
3. Add a payment method and enable **Worry-Free Mode**
4. In the left sidebar, click **API Key**
5. Click **Create API Key**
6. Copy your key — it will be in the format `sk-xxxx`

> **Important:** The Singapore region uses a different API endpoint:
> `https://dashscope-intl.aliyuncs.com`

![Qwen API Key creation page](images/step3-api-key.png)

---
 
## Step 3 — Install and Configure CCR

### Install CCR

```
npm install -g @musistudio/claude-code-router
```

![Installing CCR via npm](images/step2-ccr-install.png)

Verify it works:

```
ccr --version
```

![CCR version check](images/step2-ccr-version.png)

### Configure CCR

Open the config file:

**Windows Command Prompt:**
```
notepad %USERPROFILE%\.claude-code-router\config.json
```

**WSL / Linux terminal:**
```
nano ~/.claude-code-router/config.json
```

![Opening CCR config](images/step4-open-config.png)

Paste the following (replace with your actual Qwen API key):

```json
{
  "LOG": true,
  "LOG_LEVEL": "info",
  "HOST": "127.0.0.1",
  "PORT": 3456,
  "API_TIMEOUT_MS": 600000,
  "Providers": [
    {
      "name": "qwen",
      "api_base_url": "https://dashscope-intl.aliyuncs.com/compatible-mode/v1/chat/completions",
      "api_key": "sk-your-api-key-here",
      "models": [
        "qwen3-coder-plus",
        "qwen3-235b-a22b",
        "qwen3-max",
        "qwen3-plus"
      ]
    }
  ],
  "Router": {
    "default": "qwen,qwen3-coder-plus",
    "background": "qwen,qwen3-coder-plus",
    "think": "qwen,qwen3-coder-plus",
    "longContext": "qwen,qwen3-coder-plus",
    "longContextThreshold": 60000,
    "webSearch": "qwen,qwen3-coder-plus"
  }
}
```

![CCR config filled in](images/step4-config-filled.png)

Save the file (`Ctrl+S` on Notepad, `Ctrl+O` then `Enter` on nano).

---
 
## Step 4 — Start the CCR Server

```
ccr start
```

![Running ccr start](images/step5-ccr-start.png)

To confirm it is running, open another terminal and type:

```
ccr status
```

![CCR status output](images/step5-ccr-status.png)

You should see:

```
✅ Status: Running
🌐 Port: 3456
📡 API Endpoint: http://127.0.0.1:3456
```

---
 
## Step 5 — Point Claude CLI to CCR

Claude CLI reads two environment variables to know where to send requests:

| Variable | Value |
|----------|-------|
| `ANTHROPIC_BASE_URL` | `http://127.0.0.1:3456` — your local CCR server |
| `ANTHROPIC_API_KEY` | Your Qwen API key (`sk-xxxx` from Step 2) |

### Set for the current session only

**Windows Command Prompt:**
```
set ANTHROPIC_BASE_URL=http://127.0.0.1:3456
set ANTHROPIC_API_KEY=sk-your-qwen-key-here
```

**WSL / Linux terminal:**
```
export ANTHROPIC_BASE_URL=http://127.0.0.1:3456
export ANTHROPIC_API_KEY=sk-your-qwen-key-here
```

![Setting environment variables in terminal](images/cli-step5-env-vars.png)

> These only last for the current terminal session. See Step 6 to make them permanent.

---

## Step 6 — Make the Settings Permanent (Recommended)

### On WSL / Linux

Open your shell profile:

```
nano ~/.bashrc
```

Add these two lines at the bottom:

```
export ANTHROPIC_BASE_URL=http://127.0.0.1:3456
export ANTHROPIC_API_KEY=sk-your-qwen-key-here
```

![Adding env vars to .bashrc](images/cli-step6-bashrc.png)

Save (`Ctrl+O`, `Enter`) and exit (`Ctrl+X`), then apply:

```
source ~/.bashrc
```

### On Windows (System Environment Variables)

1. Press `Win + S`, search for **Environment Variables**, and open it
2. Under **User variables**, click **New**
3. Add `ANTHROPIC_BASE_URL` = `http://127.0.0.1:3456`
4. Add another: `ANTHROPIC_API_KEY` = your Qwen API key
5. Click **OK** and restart your terminal

![Adding system environment variables on Windows](images/cli-step6-windows-env.png)

---

## Important Notes
 
- Responses may be slow on the **free tier** — this is expected behavior
- The CCR server stops when your PC restarts — run `ccr start` again each time
- Cowork's UI will look like Claude, but Qwen is running in the background
- To switch back to Anthropic, simply select **Default** in Cowork settings
---
