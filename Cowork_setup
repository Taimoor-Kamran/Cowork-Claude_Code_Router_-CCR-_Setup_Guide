# Cowork + Claude Code Router (CCR) Setup Guide
### Qwen ya kisi bhi third-party model ke saath Cowork use karne ka tarika
 
---
 
## Prerequisites
 
Shuru karne se pehle yeh cheezein honi chahiye:
 
- Windows 10/11
- **Node.js** installed — [nodejs.org](https://nodejs.org) se download karo
- **VS Code** (optional, Cline ke liye)
- **Cowork** (Anthropic ka desktop app) installed
- Internet connection
---
 
## Step 1 — Node.js Check Karo
 
Command Prompt kholo aur likho:
 
```
node --version
```
 
Agar version aaye (jaise `v24.x.x`) toh theek hai. Agar error aaye toh nodejs.org se install karo.
 
---
 
## Step 2 — Claude Code Router Install Karo
 
```
npm install -g @musistudio/claude-code-router
```
 
Install hone ke baad check karo:
 
```
ccr --version
```
 
---
 
## Step 3 — Qwen API Key Banao
 
1. Jaiye: [modelstudio.console.alibabacloud.com](https://modelstudio.console.alibabacloud.com)
2. Account banao (Singapore region select karo)
3. Payment method add karo — Worry-Free Mode enable karo
4. Left sidebar mein **API Key** click karo
5. **Create API Key** click karo
6. Key copy karo — `sk-xxxx` format mein hogi
> **Important:** Singapore region ke liye alag API endpoint use hota hai:
> `https://dashscope-intl.aliyuncs.com`
 
---
 
## Step 4 — CCR Configure Karo
 
Notepad mein config file kholo:
 
```
notepad %USERPROFILE%\.claude-code-router\config.json
```
 
Yeh content paste karo (apni key daalo):
 
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
      "api_key": "sk-xxxx-tumhari-key",
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
 
Save karo (`Ctrl+S`).
 
---
 
## Step 5 — CCR Server Start Karo
 
```
ccr start
```
 
Status check karne ke liye:
 
```
ccr status
```
 
Output kuch aisa hoga:
 
```
✅ Status: Running
🌐 Port: 3456
📡 API Endpoint: http://127.0.0.1:3456
```
 
---
 
## Step 6 — Cowork Configure Karo
 
### Developer Mode Enable Karo
 
Cowork mein jaiye:
```
Help > Troubleshooting > Enable Developer Mode
```
 
### Third-Party Inference Configure Karo
 
Menu bar mein:
```
Developer > Configure Third-Party Inference
```
 
Yeh settings daalo:
 
| Field | Value |
|-------|-------|
| Backend | Gateway (Anthropic-compatible) |
| Gateway base URL | `http://127.0.0.1:3456` |
| Gateway API key | Tumhari Qwen key |
| Auth scheme | `bearer` |
 
**Apply locally** click karo, phir **Relaunch Now**.
 
---
 
## Step 7 — Cowork Config File Update Karo
 
Notepad mein kholo:
 
```
notepad "%LOCALAPPDATA%\Claude-3p\configLibrary\<tumhari-file-id>.json"
```
 
> File ID dhundhne ke liye:
> ```
> dir "%LOCALAPPDATA%\Claude-3p\configLibrary"
> ```
 
Yeh content daalo:
 
```json
{
  "inferenceProvider": "gateway",
  "inferenceGatewayBaseUrl": "http://127.0.0.1:3456",
  "inferenceGatewayApiKey": "sk-xxxx-tumhari-key",
  "inferenceGatewayHeaders": {
    "X-Title": "Claude-Cowork"
  },
  "inferenceGatewayDefaultModel": "qwen3-coder-plus"
}
```
 
Save karo, Cowork restart karo.
 
---
 
## Step 8 — Test Karo
 
Cowork mein type karo:
 
```
hello
```
 
Agar response aaye toh **sab kuch kaam kar raha hai!** 🎉
 
---
 
## Rozana Use Karne Ka Tarika
 
Har baar PC start karne ke baad:
 
```
ccr start
```
 
Bas itna — Cowork automatically router se connect ho jayega.
 
---
 
## Troubleshooting
 
| Problem | Solution |
|---------|----------|
| `Can't reach 127.0.0.1:3456` | `ccr start` likho CMD mein |
| `402 credits error` | API key check karo, free quota dekho |
| `invalid_api_key` | Singapore region URL use karo: `dashscope-intl` |
| Response bohat slow hai | Free tier pe normal hai, thoda wait karo |
| `Provider undefined` | config.json mein provider name check karo |
 
---
 
## Notes
 
- **Free tier** mein response slow hoga — yeh normal hai
- CCR server band ho jata hai PC restart pe — `ccr start` dobara chalao
- Cowork ka UI Claude jaisa lagega lekin peeche Qwen kaam karega
- Default Anthropic mode pe wapas jaane ke liye: Cowork settings mein **Default** select karo
---
