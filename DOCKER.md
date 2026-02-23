# Isaac – Docker Containerization

## Files structure

```
isaac-docker/
├── Dockerfile.backend    # Python/FastAPI image
├── Dockerfile.frontend   # React/Vite + Nginx image
├── nginx.conf            # Nginx config (proxy + SPA)
├── docker-compose.yml    # Orchestration
└── .env.example          # Env vars (template)
```

## Prerequisites

- Docker 24+
- Docker Compose v2
- Clone repo: `git clone https://github.com/n0mad1k/isaac.git`

## How to

### 1. Copy docker files to project root

```bash
cp Dockerfile.backend Dockerfile.frontend docker-compose.yml nginx.conf /path/to/isaac/
cp .env.example /path/to/isaac/.env
```

### 2. Set environment variables

```bash
# Edit .env with configs
nano .env
```

### 3. Run with docker

```bash
docker compose up -d
```

### 4. Access web UI

Open `http://localhost:8080` on browser and follow the setup wizard.

---

## Useful commands

```bash
# View logs
docker compose logs -f

# Stop application
docker compose down

# Rebuild
docker compose up -d --build

# Backup data (SQLite + uploads)
docker run --rm -v isaac-data:/data -v $(pwd):/backup alpine \
  tar czf /backup/isaac-backup-$(date +%Y%m%d).tar.gz /data
```

## Notes

- SQLite db and upload data are stored in `isaac-data` (persistent volume).
- To use with Raspberry Pi (ARM), the images `python:3.11-slim` and `node:20-alpine` are compatible with `linux/arm64` and `linux/arm/v7`.
- CalDAV (Radicale) is commented in `docker-compose.yml` — uncomment to enable sync calendar option.