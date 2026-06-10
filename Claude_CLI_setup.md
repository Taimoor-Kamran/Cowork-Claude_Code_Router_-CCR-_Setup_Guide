
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
 
## Step 5 — Start the CCR Server
 
```
ccr start
```

![Running ccr start](images/step5-ccr-start.png)
 
To check the server status:
 
```
ccr status
```

![CCR status output](images/step5-ccr-status.png)
 
You should see output like this:
 
```
✅ Status: Running
🌐 Port: 3456
📡 API Endpoint: http://127.0.0.1:3456
```
 
---
 
## Step 6 — Configure Cowork
 
### Enable Developer Mode
 
Inside Cowork, navigate to:
```
Help > Troubleshooting > Enable Developer Mode
```

![Enabling Developer Mode in Cowork](images/step6-developer-mode.png)
 
### Configure Third-Party Inference
 
From the menu bar:
```
Developer > Configure Third-Party Inference
```

![Opening Third-Party Inference settings](images/step6-third-party-menu.png)
 
Enter the following settings:
 
| Field | Value |
|-------|-------|
| Backend | Gateway (Anthropic-compatible) |
| Gateway base URL | `http://127.0.0.1:3456` |
| Gateway API key | Your Qwen API key |
| Auth scheme | `bearer` |
 
Click **Apply Changes**, then **Relaunch Now**.

![Third-Party Inference settings filled in](images/step6-third-party-filled.png)

 
---
 
## Step 7 — Test It
 
Type the following in Cowork:
 
```
hello
```
 
If you get a response, everything is working correctly!

![Cowork responding to hello message](images/step8-test-response.png)
 
---
 
## Daily Usage
 
Every time you restart your PC, simply run:
 
```
ccr start
```

![Running ccr start on daily use](images/daily-ccr-start.png)
 
That's it — Cowork will automatically connect to the router.
 
---
 
## Troubleshooting
 
| Problem | Solution |
|---------|----------|
| `Can't reach 127.0.0.1:3456` | Run `ccr start` in Command Prompt |
| `402 credits error` | Check your API key and free quota |
| `invalid_api_key` | Make sure you're using the Singapore endpoint: `dashscope-intl` |
| Response is very slow | This is normal on the free tier — just wait a moment |
| `Provider undefined` | Check the provider name in your config.json |
 
---
 
## Important Notes
 
- Responses may be slow on the **free tier** — this is expected behavior
- The CCR server stops when your PC restarts — run `ccr start` again each time
- Cowork's UI will look like Claude, but Qwen is running in the background
- To switch back to Anthropic, simply select **Default** in Cowork settings
---
