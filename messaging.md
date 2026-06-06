# Slack And Telegram Messaging

The digest can be scheduled and pushed to Slack or Telegram instead of only writing a desktop file.

## Slack

1. In Slack, create an incoming webhook for the channel where you want updates.
2. Copy the webhook URL.
3. Set it as an environment variable:

```powershell
$env:SLACK_WEBHOOK_URL="https://hooks.slack.com/services/..."
```

4. Run the digest:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -Days 7 -PerTopic 5
```

You can also pass it directly:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -SlackWebhook "https://hooks.slack.com/services/..."
```

## Telegram

1. Open Telegram and message `@BotFather`.
2. Create a bot with `/newbot`.
3. Copy the bot token.
4. Add the bot to a group or message it directly.
5. Get your chat ID. A simple way is to send a message to the bot, then open:

```text
https://api.telegram.org/botYOUR_BOT_TOKEN/getUpdates
```

Look for `chat.id`.

6. Set the values:

```powershell
$env:TELEGRAM_BOT_TOKEN="123456:your-bot-token"
$env:TELEGRAM_CHAT_ID="123456789"
```

7. Run the digest:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -Days 7 -PerTopic 5
```

## Scheduled Runs

For permanent scheduling, save `SLACK_WEBHOOK_URL`, `TELEGRAM_BOT_TOKEN`, and `TELEGRAM_CHAT_ID` as user environment variables, then create the Windows scheduled task in [scheduling-windows.md](scheduling-windows.md).

Keep tokens and webhook URLs private. Do not commit them to GitHub.
