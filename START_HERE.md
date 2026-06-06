# Start Here: Automate The Research Digest

This guide is for a beginner. Follow one path:

- Path A: run from your Windows computer every day
- Path B: run from GitHub every day

Use Path B if you want the automation to work even when your computer is switched off.

## What You Need

- The repo folder on your computer
- A Slack incoming webhook URL, if posting to Slack
- A Telegram bot token and chat ID, if posting to Telegram

The repo folder is:

```text
C:\Users\USER\Documents\Codex\2026-06-06\files-mentioned-by-the-user-screenshot\outputs\research-news-digest-provider
```

## Step 1: Open PowerShell In The Repo

1. Press `Windows + S`.
2. Search for `PowerShell`.
3. Open PowerShell.
4. Run:

```powershell
cd C:\Users\USER\Documents\Codex\2026-06-06\files-mentioned-by-the-user-screenshot\outputs\research-news-digest-provider
```

## Step 2: Test The Digest Locally

Run this first. It does not need Slack or Telegram.

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -ResourcesOnly -Output .\examples\resources_only.md
```

If it says `Wrote .\examples\resources_only.md`, the repo is working.

## Step 3: Choose Where To Post

You can use Slack, Telegram, or both.

### Slack Setup

1. In Slack, create an incoming webhook for your channel.
2. Copy the webhook URL. It starts with:

```text
https://hooks.slack.com/services/
```

3. In PowerShell, run:

```powershell
[Environment]::SetEnvironmentVariable("SLACK_WEBHOOK_URL", "PASTE_YOUR_SLACK_WEBHOOK_HERE", "User")
```

Or use the setup wizard:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\setup_slack.ps1
```

### Telegram Setup

1. Open Telegram.
2. Search for `@BotFather`.
3. Send `/newbot`.
4. Follow the prompts and copy the bot token.
5. Send a message to your new bot, or add it to a group and send a message there.
6. Open this link in your browser, replacing the token:

```text
https://api.telegram.org/botPASTE_YOUR_BOT_TOKEN_HERE/getUpdates
```

7. Find `chat":{"id":...}` and copy the number.
8. In PowerShell, run:

```powershell
[Environment]::SetEnvironmentVariable("TELEGRAM_BOT_TOKEN", "PASTE_YOUR_TELEGRAM_BOT_TOKEN_HERE", "User")
[Environment]::SetEnvironmentVariable("TELEGRAM_CHAT_ID", "PASTE_YOUR_TELEGRAM_CHAT_ID_HERE", "User")
```

## Step 4: Open A New PowerShell Window

Close PowerShell and open it again. This lets PowerShell see the new environment variables.

Go back to the repo:

```powershell
cd C:\Users\USER\Documents\Codex\2026-06-06\files-mentioned-by-the-user-screenshot\outputs\research-news-digest-provider
```

## Step 5: Send A Test Message

Run:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\test_messaging_config.ps1 -SendTestMessage
```

Check Slack or Telegram. You should receive a test digest.

## Step 6: Install Daily Automation On Windows

Run this to post every day at 8:00 AM:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\install_windows_task.ps1 -Time "08:00" -Days 7 -PerTopic 5 -Force
```

That is all for Windows automation.

## Optional: GitHub Automation

Use this if you want the digest to run even when your computer is off.

1. Create a new GitHub repository.
2. Upload this repo folder to GitHub.
3. In GitHub, open your repo.
4. Go to `Settings > Secrets and variables > Actions`.
5. Add repository secrets:

```text
SLACK_WEBHOOK_URL
TELEGRAM_BOT_TOKEN
TELEGRAM_CHAT_ID
```

6. Go to `Actions`.
7. Open `Scheduled Digest`.
8. Click `Run workflow` to test it.

The scheduled workflow runs every day at 8:00 AM IST.

## Common Problems

If `test_messaging_config.ps1` says Slack and Telegram are false, open a new PowerShell window and try again.

If Telegram does not send, make sure you sent at least one message to your bot first.

If Slack does not send, check that your webhook URL starts with `https://hooks.slack.com/services/`.

If Telegram says `401 Unauthorized`, your bot token is wrong or still the example value. Go back to `@BotFather`, copy the real token, set `TELEGRAM_BOT_TOKEN` again, then open a new PowerShell window.

If Telegram says `chat not found`, run:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\find_telegram_chat_id.ps1
```

Copy the `ChatId` value it prints, save it as `TELEGRAM_CHAT_ID`, then open a new PowerShell window.

You can also use the setup wizard:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\setup_telegram.ps1
```

Never upload bot tokens or webhook URLs into public files.
