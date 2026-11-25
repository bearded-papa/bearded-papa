<div align="center">

# 🏠 Paul's Homelab

*A small, hands-on self-hosted setup: one mini PC, two Raspberry Pis, two VPSes.*

[Hardware](#-hardware) · [Services](#-services) · [Infrastructure](#-infrastructure) · [Docs](#-docs-and-code) · [History](#-history)

</div>

> Home is behind CGNAT, so everything public goes out through a tunnel (Pangolin), never port-forwards. Most links below are login-gated.

## 🖥️ Hardware

| Machine | Spec | Role |
|---|---|---|
| **dell-server** | Dell OptiPlex 3060 Micro, i5-8500T, 8 GB, Ubuntu | Main Docker host; exports its drives over NFS |
| **Drives** | 500 GB SSD + two 4 TB USB drives | App data, media, backups |
| **pi4** | Raspberry Pi 4, 8 GB | Backups, files, web terminal, git, ntfy, the Handbook |
| **pi5-test** | Raspberry Pi 5 | Test server: try it here first |
| **VPS x2** | RackNerd, Debian 13 | Public edge (Pangolin) and always-on services |

## 📦 Services

### 🎬 Media
| App | What it does |
|---|---|
| [Jellyfin](https://jellyfin.org/) | Media server |
| [Sonarr](https://sonarr.tv/) · [Radarr](https://radarr.video/) · [Prowlarr](https://prowlarr.com/) | TV, movies and indexers |
| [qBittorrent](https://www.qbittorrent.org/) | Downloads |
| [Seerr](https://github.com/seerr-team/seerr) | Requests for family and friends |
| [Cleanuparr](https://github.com/Cleanuparr/Cleanuparr) · [Reclaimerr](https://github.com/jessielw/reclaimerr) | Queue and library tidying |

### 📷 Files and photos
| App | What it does |
|---|---|
| [Immich](https://immich.app/) ([live](https://immich.pauloakes.uk)) | Photos |
| [OpenCloud](https://opencloud.eu/) | File sync and sharing |
| [nextExplorer](https://nextexplorer.pauloakes.uk) | Web file manager |

### 🧰 Everyday
| App | What it does |
|---|---|
| [Mealie](https://mealie.io/) | Recipes |
| [FreshRSS](https://freshrss.org/) | RSS reader |
| [GeoPulse](https://geopulse.pauloakes.uk) | Location history (Life360 replacement) |
| Bus tracker | Live bus map using Bus Open Data Service |

### 🛠️ Ops
| App | What it does |
|---|---|
| [Homepage](https://gethomepage.dev/) | The dashboard this page is modelled on |
| [Arcane](https://getarcane.app/) | Docker deployments from Git |
| [Beszel](https://beszel.pauloakes.uk) | Host monitoring |
| [Scrutiny](https://scrutiny.pauloakes.uk) | Drive SMART health |
| [Borg UI](https://borg-ui.pauloakes.uk) | Backups |
| [Gotify](https://gotify.pauloakes.uk) · [ntfy](https://ntfy.pauloakes.uk) | Notifications |
| [Termix](https://terminal.pauloakes.uk) | Web SSH |

### 🔐 Edge and identity
| App | What it does |
|---|---|
| [Pangolin](https://github.com/fosrl/pangolin) | Tunnelled public access with SSO |
| [Pocket ID](https://id.pauloakes.uk) | Passkey login (OIDC) |
| [Tailscale](https://tailscale.com/) | Private network, Tailnet Lock on |

## 🔗 Infrastructure

- **Deploys:** Arcane Git Sync from a private repo of Compose stacks. Bind mounts only, memory limits on heavy containers.
- **Storage:** Pis mount the Dell's drives over NFS.
- **Backups:** Borg, with SQLite apps stopped around the nightly run. Off-site copy is next.
- **Alerts:** Beszel plus UptimeRobot, delivered to Gotify.

## 📚 Docs and code

| What | Where |
|---|---|
| Git hosting | Forgejo (moving over from Gitea), mirroring from GitHub |
| Homelab Handbook | Interactive fix-it guides, checklists and rebuild steps, hosted on the Pi 4 |
| Bus tracker | Private repo, hosted on the Pi 4 |
| This profile | [previous_setups.md](previous_setups.md) lists apps I tried and dropped |

## 🕰️ History

Earlier versions ran on [Komodo](https://komo.do/), with Dockge before that. The old README is kept in [README_OLD.md](README_OLD.md). The move to Arcane, Pangolin and Pocket ID came in autumn 2026, along with a rebuild of both VPSes.
