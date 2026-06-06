# Research News Digest Provider

Automated news and learning-resource digest for emerging wireless, UAV, vehicular-network, and autonomous-systems research.

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

## Webhook Posting

Set a webhook URL, then run the provider:

```powershell
$env:DIGEST_WEBHOOK_URL="https://your-webhook-url"
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -Days 7 -PerTopic 5
```

For details, see [docs/webhooks.md](docs/webhooks.md).

## Customize Topics

Edit [config/topics.json](config/topics.json). Each topic has:

- `name`: digest section title
- `query`: news/paper search query
- `why`: short reason this topic belongs in the digest
- `resources`: free learning links posted with the topic

## Automate

Windows Task Scheduler instructions are in [docs/scheduling-windows.md](docs/scheduling-windows.md).

GitHub Actions smoke testing is included in [.github/workflows/smoke-test.yml](.github/workflows/smoke-test.yml).

## Repository Layout

```text
.
├── .github/workflows/smoke-test.yml
├── config/topics.json
├── docs/
├── examples/resources_only.md
├── scripts/digest_provider.ps1
├── scripts/digest_provider.py
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

## License

MIT. See [LICENSE](LICENSE).
