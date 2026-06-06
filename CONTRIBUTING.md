# Contributing

Contributions are welcome.

Good additions include:

- new topic definitions in `config/topics.json`
- better free learning resources
- improved feed parsing
- examples for classroom, lab, or newsletter workflows

Please keep links educational, accessible, and preferably free.

## Local Smoke Test

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\digest_provider.ps1 -ResourcesOnly -Output .\examples\resources_only.md
```

If Python is installed:

```powershell
python .\scripts\digest_provider.py --resources-only --output .\examples\resources_only.md
```
