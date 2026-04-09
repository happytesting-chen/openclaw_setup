# OpenClaw Setup Guide

## Step 1: Install OpenClaw

Run the following command to install OpenClaw:

```bash
curl -fsSL https://openclaw.ai/install.sh | bash
```

---

## Step 2: Onboard OpenClaw

Run the onboard command to initialize OpenClaw and install the daemon:

```bash
openclaw onboard --install-daemon
```

During this process, you will be prompted to choose a model. All other settings can be configured later.

> **Note:** The setup wizard generates a gateway token by default, even for loopback (local) connections. This means local clients must authenticate before connecting. This prevents other local processes from calling your Gateway without permission.

After onboarding, you can verify the OpenClaw gateway is running:

```bash
ps aux | grep openclaw
```

To open the web dashboard, navigate to the following URL in your browser:

```
http://127.0.0.1:18789
```

---

## Step 3: Set Up Telegram Bot

### 3.1 Create a Bot via BotFather

1. Open Telegram and message **@BotFather**
2. Run the command `/newbot`
3. Choose:
   - A **display name** for your bot
   - A **unique bot username** ending in `bot` (e.g. `myopenclaw_bot`)
4. BotFather will provide you with a **bot token**

### 3.2 Configure the Bot Token in OpenClaw

The default OpenClaw configuration file is located at:

```
~/.openclaw/openclaw.json
```

Add the token to your OpenClaw configuration:

```json
"channels": {
  "telegram": {
    "enabled": true,
    "botToken": "YOUR_BOT_TOKEN_HERE",
    "dmPolicy": "pairing",
    "groups": {
      "*": {
        "requireMention": true
      }
    }
  }
}
```

Replace `YOUR_BOT_TOKEN_HERE` with the token provided by BotFather.

> **Note:** After configuring `openclaw.json`, restart the OpenClaw gateway for changes to take effect:

```bash
openclaw gateway restart
```

---

## Step 4: Pair the Telegram Bot (First-Time Use)

1. Open your Telegram bot and send: `hi`
2. The bot will respond with a pairing code
3. Run the following command in your terminal, replacing `xxxx` with your pairing code:

```bash
openclaw pairing approve telegram xxxx
```

Once paired, you can start chatting with OpenClaw directly through your Telegram bot.
