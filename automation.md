# Automation Guide

You can automate the digest in two ways:

- local Windows Task Scheduler
- GitHub Actions scheduled workflow

Use local scheduling if your PC is usually online. Use GitHub Actions if you want the digest to run from GitHub without depending on your desktop.

## Option 1: Windows Task Scheduler

From the repository root, set your destination secrets.

Slack:

```powershell
[Environment]::SetEnvironmentVariable("SLACK_WEBHOOK_URL", "https://hooks.slack.com/services/...", "User")
```

Telegram:

```powershell
[Environment]::SetEnvironmentVariable("TELEGRAM_BOT_TOKEN", "123456:your-bot-token", "User")
[Environment]::SetEnvironmentVariable("TELEGRAM_CHAT_ID", "123456789", "User")
```

Open a new PowerShell window so it can see the updated environment variables.

Check the config:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\test_messaging_config.ps1
```

Send a test digest:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\test_messaging_config.ps1 -SendTestMessage
```

Install the daily task:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\install_windows_task.ps1 -Time "08:00" -Days 7 -PerTopic 5 -Force
```

The task reads `SLACK_WEBHOOK_URL`, `TELEGRAM_BOT_TOKEN`, and `TELEGRAM_CHAT_ID` automatically.

## Option 2: GitHub Actions

Push this repository to GitHub.

In your GitHub repo, go to:

```text
Settings > Secrets and variables > Actions > New repository secret
```

Add the secrets you want:

```text
SLACK_WEBHOOK_URL
TELEGRAM_BOT_TOKEN
TELEGRAM_CHAT_ID
```

The workflow at `.github/workflows/scheduled-digest.yml` runs every day at `02:30 UTC`, which is `08:00 IST`.

You can also run it manually:

```text
Actions > Scheduled Digest > Run workflow
```

## Which Should You Use?

Use GitHub Actions if you want the digest to run even when your desktop is off.

Use Windows Task Scheduler if you want everything to stay local on your machine.
