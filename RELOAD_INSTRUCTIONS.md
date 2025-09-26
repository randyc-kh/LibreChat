# LibreChat Reload Instructions

## Quick Reload (Configuration Changes Only)
When you've modified `librechat.yaml` or `.env` files:

```bash
# Restart just the LibreChat container
docker compose restart api

# Or if you want to see logs during restart
docker compose restart api && docker compose logs -f api
```

## Full Reload (After Docker Changes)
When you've modified `docker-compose.yml` or `docker-compose.override.yml`:

```bash
# Stop all services
docker compose down

# Start all services fresh
docker compose up -d

# Check status
docker compose ps
```

## Nuclear Reload (Complete Fresh Start)
When you want to completely reset everything:

```bash
# Stop and remove everything including volumes
docker compose down -v

# Remove all local data directories
rm -rf logs data uploads images meili_data_v1.12 data-node

# Recreate directories
mkdir -p logs data uploads images

# Start fresh
docker compose up -d
```

## Check Status Commands
```bash
# See all container status
docker compose ps

# View LibreChat logs
docker compose logs api --tail=20

# Follow logs in real-time
docker compose logs -f api
```

## What Gets Reloaded
- ✅ **Configuration changes** (`librechat.yaml`, `.env`) → Quick reload
- ✅ **MCP server connections** → Automatic reconnection
- ✅ **Ollama model discovery** → Happens on startup
- ✅ **Volume mounts** → Full reload needed
- ✅ **Docker compose changes** → Full reload needed
