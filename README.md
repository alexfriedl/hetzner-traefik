# Hetzner Traefik Reverse Proxy

Traefik v3 reverse proxy mit automatischen Let's Encrypt SSL-Zertifikaten.

## Laufende Services

| Service | URL | Zugriff |
|---------|-----|---------|
| Scraper | https://hetzner.cwwk.cloud/dashboard | Öffentlich |
| CV-Service | https://hetzner.cwwk.cloud/cv/ | Öffentlich |
| Bewerber | https://hetzner.cwwk.cloud/bewerber/ | Öffentlich |
| cAdvisor | https://hetzner.cwwk.cloud/cadvisor/ | Öffentlich |
| Traefik Dashboard | http://100.71.98.104:8080/dashboard/ | Nur Tailscale |

## Server

- **IP:** 46.225.93.23
- **Domain:** hetzner.cwwk.cloud
- **Tailscale IP:** 100.71.98.104

## Firewall

Offene Ports (öffentlich):
- 22 (SSH)
- 80 (HTTP → Redirect zu HTTPS)
- 443 (HTTPS)

Interne Ports (nur Tailscale):
- 8080 (Traefik Dashboard)

## Setup

```bash
# SSH zum Server
ssh root@46.225.93.23

# Traefik neustarten
cd /opt/traefik
docker-compose down && docker-compose up -d

# Logs anschauen
docker logs traefik -f
```

## Dateien auf dem Server

```
/opt/traefik/
├── docker-compose.yml
├── traefik.yml
├── dynamic.yml
└── acme.json (SSL-Zertifikate)

/opt/scraper/
└── docker-compose.yml

/opt/cv-service/
└── docker-compose.yml

/opt/monitoring/
└── docker-compose.yml
```
