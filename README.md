# Research News Digest Provider

Automated news and learning-resource digest for emerging wireless, UAV, vehicular-network, and autonomous-systems research.

New to this? Start with [START_HERE.md](START_HERE.md).

The default topic set was built from screenshots covering:

- 6G, Open RAN, Open6G, and open-source wireless testbeds
- OpenAirInterface and open-source 5G core/RAN stacks
- spectrum sharing, integrated sensing, clock distribution, and positioning
- vehicular networks, sidelink, VANET, C-V2X, and collision avoidance
- UAV AI, object detection, hyperspectral imaging, and remote sensing
- autonomous transport, LiDAR, traffic-sign recognition, and EV systems

Each digest includes recent news/papers plus free educational resources for every topic.

## Features

- No paid API key required
- Uses Google News RSS and arXiv Atom feeds
- Includes curated free courses, documentation, datasets, and tutorials
- Supports PowerShell and Python
- Can post to Discord or Slack-style webhooks
- Ready for Windows Task Scheduler or GitHub Actions

## Quick Start

Run from the repository root:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -Days 7 -PerTopic 5 -Output .\latest_digest.md
```

Generate only the educational resources:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -ResourcesOnly -Output .\resources_only.md
```

If Python is available:

```powershell
python .\scripts\digest_provider.py --days 7 --per-topic 5 --output .\latest_digest.md
```

## Slack Or Telegram Posting

Slack:

```powershell
$env:SLACK_WEBHOOK_URL="https://hooks.slack.com/services/..."
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -Days 7 -PerTopic 5
```

Telegram:

```powershell
$env:TELEGRAM_BOT_TOKEN="123456:your-bot-token"
$env:TELEGRAM_CHAT_ID="123456789"
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -Days 7 -PerTopic 5
```

For setup details, see [docs/messaging.md](docs/messaging.md).

## Customize Topics

Edit [config/topics.json](config/topics.json). Each topic has:

- `name`: digest section title
- `query`: news/paper search query
- `why`: short reason this topic belongs in the digest
- `resources`: free learning links posted with the topic

## Automate

Step-by-step Slack/Telegram automation is in [docs/automation.md](docs/automation.md).

Windows Task Scheduler instructions are also in [docs/scheduling-windows.md](docs/scheduling-windows.md).

Common setup errors are covered in [docs/troubleshooting.md](docs/troubleshooting.md).

GitHub Actions smoke testing is included in [.github/workflows/smoke-test.yml](.github/workflows/smoke-test.yml).

Daily GitHub Actions posting is included in [.github/workflows/scheduled-digest.yml](.github/workflows/scheduled-digest.yml).

## Repository Layout

```text
.
├── .github/workflows/smoke-test.yml
├── .github/workflows/scheduled-digest.yml
├── config/topics.json
├── docs/
├── examples/resources_only.md
├── scripts/install_windows_task.ps1
├── scripts/test_messaging_config.ps1
├── scripts/find_telegram_chat_id.ps1
├── scripts/setup_telegram.ps1
├── scripts/setup_slack.ps1
├── scripts/digest_provider.ps1
├── scripts/digest_provider.py
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## License

MIT. See [LICENSE](LICENSE).
