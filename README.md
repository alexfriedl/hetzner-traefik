# Hetzner Traefik Reverse Proxy

Traefik v3 reverse proxy with automatic Let's Encrypt SSL certificates.

## Setup

```bash
# Create traefik network
docker network create traefik

# Create acme.json for certificates
touch acme.json && chmod 600 acme.json

# Start traefik
docker compose up -d
```

## Add services to Traefik

Add these labels to any docker container to expose it via Traefik:

```yaml
labels:
  - "traefik.enable=true"
  - "traefik.http.routers.myservice.rule=Host(`myservice.hetzner.cwwk.cloud`)"
  - "traefik.http.routers.myservice.entrypoints=websecure"
  - "traefik.http.routers.myservice.tls.certresolver=letsencrypt"
  - "traefik.http.services.myservice.loadbalancer.server.port=3000"
networks:
  - traefik

networks:
  traefik:
    external: true
```

## Connect existing containers

```bash
# Connect a running container to traefik network
docker network connect traefik <container_name>
```

## Dashboard

Access: https://traefik.hetzner.cwwk.cloud
- User: admin
- Password: admin (CHANGE THIS!)

## Services

| Service | URL |
|---------|-----|
| Traefik Dashboard | https://traefik.hetzner.cwwk.cloud |
| Scraper | https://scraper.hetzner.cwwk.cloud |
| Auto-Bewerber | https://bewerber.hetzner.cwwk.cloud |
| CV-Service | https://cv.hetzner.cwwk.cloud |
| cAdvisor | https://cadvisor.hetzner.cwwk.cloud |
