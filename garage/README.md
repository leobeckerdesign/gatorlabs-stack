# Garage S3 — GatorLabs

Single-node Garage object storage for the GatorLabs demo stack.

## Build

```bash
docker build -t garage-gatorlabs ./garage
```

## Run

The TOML config is supplied at runtime via the `GARAGE_CONFIG_B64` environment variable (base64-encoded). This keeps secrets out of the image and the repo. See the Dokploy compose for the exact env values.

## Required env vars

- `GARAGE_CONFIG_B64` — base64 of the full `garage.toml` (including rpc_secret, admin_token, metrics_token)
- `TZ` — timezone, e.g. `America/Sao_Paulo`

## Ports

- `3900` — S3 API
- `3901` — RPC (cluster, not exposed externally)
- `3903` — Admin API
