# Windows Scheduling

Create a daily scheduled task that writes `latest_digest.md` every morning at 8:00 AM and posts to Slack/Telegram when messaging environment variables are configured.

The easiest way is to use the installer script:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\install_windows_task.ps1 -Time "08:00" -Days 7 -PerTopic 5 -Force
```

To verify messaging first:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\test_messaging_config.ps1 -SendTestMessage
```

## Manual Setup

Run PowerShell from the repository root:

```powershell
$repo = (Get-Location).Path
$script = Join-Path $repo "scripts\digest_provider.ps1"
$output = Join-Path $repo "latest_digest.md"

$action = New-ScheduledTaskAction `
  -Execute "powershell.exe" `
  -Argument "-NoProfile -ExecutionPolicy Bypass -File `"$script`" -Days 7 -PerTopic 5 -Output `"$output`"" `
  -WorkingDirectory $repo

$trigger = New-ScheduledTaskTrigger -Daily -At 8:00AM

Register-ScheduledTask `
  -TaskName "ResearchNewsDigest" `
  -Action $action `
  -Trigger $trigger `
  -Description "Daily research news digest for 6G, UAV, VANET, and autonomous systems"
```

To post somewhere instead of only writing a local file, set one of these as user environment variables before creating the task:

```powershell
[Environment]::SetEnvironmentVariable("SLACK_WEBHOOK_URL", "https://hooks.slack.com/services/...", "User")
[Environment]::SetEnvironmentVariable("TELEGRAM_BOT_TOKEN", "123456:your-bot-token", "User")
[Environment]::SetEnvironmentVariable("TELEGRAM_CHAT_ID", "123456789", "User")
```

Then create the scheduled task normally. The script reads those variables when the task runs.
