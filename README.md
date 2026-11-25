<div align="center">

# 🏠 Paul's Homelab

*A small, hands-on self-hosted setup: one mini PC, two Raspberry Pis, two VPSes.*

[Hardware](#-hardware) · [Services](#-services) · [Infrastructure](#-infrastructure) · [Docs](#-docs-and-code) · [History](#-history)

</div>

> The *Compose* links open the stack folder in my private `server-blueprint` repo, so they only load for me. Home is behind CGNAT, so everything public goes out through a tunnel (Pangolin), never port-forwards. Most links below are login-gated.

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
| App | What it does | Compose |
|---|---|---|
| [Jellyfin](https://jellyfin.org/) | Media server | [media_stack](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/media_stack) |
| [Sonarr](https://sonarr.tv/) · [Radarr](https://radarr.video/) · [Prowlarr](https://prowlarr.com/) | TV, movies and indexers | [media_stack](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/media_stack) |
| [qBittorrent](https://www.qbittorrent.org/) | Downloads | [media_stack](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/media_stack) |
| [Seerr](https://github.com/seerr-team/seerr) | Requests for family and friends | [media_stack](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/media_stack) |
| [Cleanuparr](https://github.com/Cleanuparr/Cleanuparr) · [Reclaimerr](https://github.com/jessielw/reclaimerr) | Queue and library tidying | [media_stack](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/media_stack) |

### 📷 Files and photos
| App | What it does | Compose |
|---|---|---|
| [Immich](https://immich.app/) ([live](https://immich.pauloakes.uk)) | Photos | [immich](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/immich) |
| [OpenCloud](https://opencloud.eu/) | File sync and sharing | [opencloud](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/opencloud) |
| [nextExplorer](https://nextexplorer.pauloakes.uk) | Web file manager | [nextexplorer](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/nextexplorer) |

### 🧰 Everyday
| App | What it does | Compose |
|---|---|---|
| [Mealie](https://mealie.io/) | Recipes | [mealie](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/mealie) |
| [GeoPulse](https://geopulse.pauloakes.uk) | Location history (Life360 replacement) | [geopulse](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/geopulse) |
| Bus tracker | Live bus map using Bus Open Data Service | [bus-tracker](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/bus-tracker) |

### 🛠️ Ops
| App | What it does | Compose |
|---|---|---|
| [Homepage](https://gethomepage.dev/) | The dashboard this page is modelled on | [homepage](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/homepage) |
| [Arcane](https://getarcane.app/) | Docker deployments from Git | — |
| [Beszel](https://beszel.pauloakes.uk) | Host monitoring | [beszel](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/beszel) |
| [Scrutiny](https://scrutiny.pauloakes.uk) | Drive SMART health | [scrutiny](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/scrutiny) |
| [Borg UI](https://borg-ui.pauloakes.uk) | Backups | [borg-ui](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/borg-ui) |
| [Gotify](https://gotify.pauloakes.uk) · [ntfy](https://ntfy.pauloakes.uk) | Notifications | [gotify](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/gotify) · [ntfy](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/ntfy) |
| [Termix](https://terminal.pauloakes.uk) | Web SSH | [termix](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/termix) |

### 🔐 Edge and identity
| App | What it does | Compose |
|---|---|---|
| [Pangolin](https://github.com/fosrl/pangolin) | Tunnelled public access with SSO | [pangolin-site](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/pangolin-site) |
| [Pocket ID](https://id.pauloakes.uk) | Passkey login (OIDC) | [pocket-id](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/pocket-id) |
| [Tailscale](https://tailscale.com/) | Private network, Tailnet Lock on | — |

## 🔗 Infrastructure

- **Deploys:** Arcane Git Sync from a private repo of Compose stacks. Bind mounts only, memory limits on heavy containers.
- **Storage:** Pis mount the Dell's drives over NFS.
- **Backups:** Borg, with SQLite apps stopped around the nightly run. Off-site copy is next.
- **Alerts:** Beszel plus UptimeRobot, delivered to Gotify.

## 📚 Docs and code

| What | Where |
|---|---|
| Git hosting | Forgejo (moving over from Gitea), mirroring from GitHub, stack: [forgejo](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/forgejo) |
| Homelab Handbook | Interactive fix-it guides, checklists and rebuild steps, hosted on the Pi 4 ([repo](https://github.com/bearded-papa/homelab-handbook), stack: [handbook](https://github.com/bearded-papa/server-blueprint/tree/main/stacks/handbook)) |
| Bus tracker | Private repo, hosted on the Pi 4 |
| This profile | [previous_setups.md](previous_setups.md) lists apps I tried and dropped |

## 🕰️ History

Earlier versions ran on [Komodo](https://komo.do/), with Dockge before that. The old README is kept in [README_OLD.md](README_OLD.md). The move to Arcane, Pangolin and Pocket ID came in autumn 2026, along with a rebuild of both VPSes.
