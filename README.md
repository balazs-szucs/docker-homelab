# My Homelab Setup

I built this self-hosted infrastructure using Docker containers. It handles everything from automatic SSL certificates to monitoring, with a focus on keeping things secure and easy to manage.

## What It Does

This homelab includes:
- Automatic SSL certificates through Let's Encrypt and Cloudflare
- User authentication with optional two-factor support
- Reverse proxy that routes all traffic and manages services
- Auto-updates for all containers
- Monitoring and logs for everything running

![Homelab Architecture](images/diagram.svg)

## How It's Built

I organized everything into separate groups that each handle different jobs:

### Security & Network (`edge.yml`)
- Traefik: Routes traffic and handles SSL automatically
- Authelia: Manages logins and two-factor authentication
- CrowdSec: Watches for suspicious activity and blocks threats

### Apps (`media.yml`)
- Jellyfin: Streams movies and TV shows
- Kavita: Manages my digital book library
- Komga: Organizes comics and manga

### Monitoring & Tools (`utils.yml`)
- Dozzle: Watch logs from all containers in real-time
- Uptime Kuma: Checks if services are running and sends alerts
- Stirling PDF: Handles PDF editing and conversion
- Pingvin Share: Share files securely with others

### Infrastructure (`infra.yml`)
- Watchtower: Keeps containers updated automatically
- Redis: Fast cache for apps that need it

### Downloads (`downloads.yml`)
- VPN Gateway: Routes specific traffic through a VPN
- Download Client: Handles torrent downloads
- Automation Tools: Organize and rename downloaded content
- Subtitle Service: Finds and downloads subtitles automatically

## Key Features

Everything as Code
- Split Docker Compose files for different service groups
- SSL certificates renew themselves automatically
- Services know about their dependencies and start in the right order

Security First
- Authentication required for sensitive services (for non-sensitive security via Crowdsec, and geoblocking)
- Some traffic routes through VPN for privacy
- CrowdSec learns what's normal and blocks weird behavior

Reliable and Self-Healing
- Health checks on every service
- Containers restart automatically if they crash
- All logs go to one place for easy troubleshooting
- Uptime monitoring

## Tech Stack

- Containers: Docker and Docker Compose
- Proxy: Traefik with Let's Encrypt, plus plugins for geoblocking, caching, and Cloudflare IP detection
- Auth: Authelia (currently using single-factor, but supports more)
- Security: CrowdSec for threat detection, WireGuard for VPN
- Networking: Docker networks with automatic service discovery


## What I Learned

- Docker: Running services in containers, writing compose files, building custom images
- Networking: Setting up reverse proxies, routing traffic through VPNs, connecting services together
- Security: Automated SSL with Traefik, user authentication with Authelia, threat blocking with CrowdSec
- Automation: Managing infrastructure with code, automatic updates, self-healing containers
- Monitoring: Collecting logs, health checks, uptime tracking