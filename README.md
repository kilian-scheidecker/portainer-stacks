# 🧱 portainer-stacks

This repository contains Docker Compose configurations for all containers deployed via Portainer stacks. It is designed for use in a self-hosted environment, running on a Proxmox-based virtual machine architecture.

All containers are defined and versioned here. Portainer monitors the repository for updates and redeploys stacks accordingly.

---

## 🧭 Architecture

- **Host VM**: `Hephaistos`  
  A virtual machine running on the `Atlas` Proxmox hypervisor.
  
- **Orchestration**:  
  Portainer is manually started on `Hephaistos`. Once running, it deploys and manages all other containers using stack definitions from this repository.

- **Stack Deployment**:  
  Each service has its own folder with a `docker-compose.yaml` file. These are configured as **Git-based stacks** in Portainer.

---

## 🔄 Update Strategy

- Renovate scans the repository every 24 hours.
- It checks for newer container image versions (excluding pre-releases).
- Pull requests are opened automatically for review before updates are merged.
- No containers use the `:latest` tag; updates are explicit and controlled.

---

## 🧰 Managed Services

The following services are defined as Portainer stacks:

- **Flaresolverr**  
  Image: `ghcr.io/flaresolverr/flaresolverr`

- **Jackett**  
  Image: `linuxserver/jackett`

- **Jellyfin**  
  Image: `jellyfin/jellyfin`

- **qBittorrent**  
  Image: `linuxserver/qbittorrent`

- **Radarr**  
  Image: `linuxserver/radarr`

- **Sonarr**  
  Image: `linuxserver/sonarr`

---

## 🔧 Portainer Stack Setup

To connect a stack in Portainer:

1. Open the Portainer UI
2. Navigate to **Stacks** → **+ Add stack**
3. Select **Git Repository**
4. Provide:
   - Repository URL: `https://github.com/kilian-scheidecker/portainer-stacks.git`
   - Compose file path (e.g., `radarr/docker-compose.yaml`)
5. Configure auto-update settings if needed

---

## 📁 Repository Structure

Each directory corresponds to a Portainer stack:

```bash
/
├── flaresolverr/
│   └── docker-compose.yaml  
├── jackett/
│   └── docker-compose.yaml  
├── jellyfin/
│   └── docker-compose.yaml  
├── qbittorrent/
│   └── docker-compose.yaml  
├── radarr/
│   └── docker-compose.yaml  
├── sonarr/
│   └── docker-compose.yaml  
├── renovate.json  
└── README.md
```

---

## 📑 Notes

- Stack deployments are fully declarative.
- Updates are only applied after manual approval of Renovate PRs.
- Portainer is the only container started directly on the host; all others are managed through it.
