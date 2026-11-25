# Paul's homelab

A small, hands-on homelab: one mini PC doing the heavy lifting, two Raspberry Pis, and a couple of cheap VPSes. Home is behind CGNAT, so everything public goes out through a tunnel rather than port-forwards.

## Hardware

| Machine | What it is | Job |
|---|---|---|
| **dell-server** | Dell OptiPlex 3060 Micro, i5-8500T, 8 GB RAM, Ubuntu | Main Docker host: media, photos, files, most apps. Exports its drives over NFS |
| **Drives** | 500 GB SSD (appdata), two 4 TB USB drives (media, data/backups) | Storage behind the Dell |
| **pi4** | Raspberry Pi 4, 8 GB, Raspberry Pi OS Lite | Backups (Borg UI), file manager, web terminal, git, this homelab's handbook |
| **pi5-test** | Raspberry Pi 5 | Spare test server: try things here before they go near production |
| **VPS x2** | RackNerd VPSes, Debian 13 | Public edge (Pangolin) and a few always-on services |

## How it fits together

- **Public access:** [Pangolin](https://github.com/fosrl/pangolin) on a VPS, with tunnel clients at home. SSO in front of most things, [Pocket ID](https://pocket-id.org/) (passkeys) as the login provider.
- **Private access:** Tailscale between all the machines, with Tailnet Lock on.
- **Deploys:** [Arcane](https://github.com/getarcaneapp/arcane) with Git Sync from a private repo of Docker Compose stacks (one folder per stack, bind mounts only, memory limits on the heavy containers).
- **Storage:** the Pis mount the Dell's drives over NFS; app data lives on the Dell.
- **Backups:** Borg (through Borg UI) to repos on the Dell's drives, with containers that use SQLite stopped around the nightly run. Off-site copies are the next job.
- **Monitoring:** Beszel for the hosts, UptimeRobot watching the VPSes from outside, alerts to Gotify.
- **Docs:** I keep an interactive "Homelab Handbook" (fix-it guides, checklists, rebuild steps) hosted on the Pi 4 and written with Claude.

## What I run

- **Media:** Jellyfin, Sonarr, Radarr, Prowlarr, qBittorrent, Seerr, Cleanuparr, Reclaimerr
- **Photos and files:** Immich, OpenCloud, nextExplorer
- **Everyday apps:** Mealie, FreshRSS, GeoPulse (location history, replacing Life360), a live bus tracker
- **Dashboards and ops:** Homepage, Arcane, Beszel, Scrutiny (SMART), Gotify, ntfy, Borg UI, Termix
- **Code:** Forgejo (moving over from Gitea)
- **Edge and identity:** Pangolin, Pocket ID, Tailscale

Things I tried and dropped are in [previous_setups.md](previous_setups.md).

## Before this

Earlier versions of this setup ran on [Komodo](https://komo.do/) (with Dockge before that) across the same Pis and VPSes. That README is kept in [README_OLD.md](README_OLD.md) for the history. The move to Arcane, Pangolin and Pocket ID came in autumn 2026, along with a rebuild of both VPSes.
