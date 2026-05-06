# Polotno Studio — GatorLabs

Open-source frontend (clone of `polotno-project/polotno-puter`) served via nginx as a static SPA. The Polotno SDK runs client-side in demo mode (free for personal/educational use; commercial use requires a paid key).

## Build

```bash
docker build -f polotno/Dockerfile -t polotno-gatorlabs .
```

## Ports

- `80` — HTTP (nginx)

## Notes

- SPA routing handled in nginx via `try_files`
- Plugin/MCP bridge for agent automation will be added in a follow-up commit.
