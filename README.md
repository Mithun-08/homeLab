# Nimbus (HomeServer)

I first started self-hosting hoping to get an ad blocker on my home 
Wi-Fi to block YouTube ads on the TV — but after digging in, I found 
that my ISP (Airtel) locks the router settings to prevent me from 
using my own DNS.

The second reason was escaping Google Drive's 15GB free tier, 40% of 
which was already eaten up by WhatsApp backups alone.

I've been doing this since December 2025.

---

## Hardware

- **Machine**: ASUS Intel N150 Mini PC
- **RAM**: 16GB
- **OS Drive**: 128GB SSD
- **Storage**: Salvaged HDD from old laptop
- **Running**: Headless, 24/7

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/207c2269-2665-4e03-b9be-e9143c3537b3" />

---

## Services

| Service | Description |
|---|---|
| **Nextcloud** | Self hosted Google Drive, without the 15GB limit |
| **OnlyOffice** | Open, edit and save files in the browser — no downloading, editing and re-uploading |
| **Immich** | Google Photos replacement |
| **Pihole** | Ad Blocker |
| **Home Assistant** | Smart home automation |
| **CouchDB** | Obsidian Vault synchronized in the cloud |
| **Beszel** | Resource monitoring for the server and containers |
| **[Uptime Kuma](https://status.mithn.in/)** | Monitors all services and alerts on downtime |
| **Portainer** | Docker management UI |
| **Watchtower** | Auto-updates all containers |
| **Gotify** | Self-hosted push notifications |
| **Cloudflared** | Cloudflare Tunnel — everything is HTTPS, zero open ports to escape CGNAT |
| **Postfix** | Self-hosted mail server — emails me on failures, restarts or updates |
| **[Wordle](https://wordly.mithn.in/)** | Forked and self-hosted with the cooldown removed |
| **[BentoPDF](https://pdf.mithn.in/)** | PDF tools |

---

## Security & Maintenance

- Zero open ports — all access goes through Cloudflare Tunnel
- Sensitive config lives in `.env` files, never in compose files
- Watchtower updates containers nightly at 4am
- Weekly cron runs `apt update && upgrade` to keep system packages fresh
- Server auto-restarts every 6 months via cron
- Postfix emails me on any failures, restarts or updates

---

## References
- [Setting up Cloudflare tunnel](https://youtu.be/ey4u7OUAF3c)
- [Setting up CouchDB for Obsidian LiveSync](https://pinggy.io/blog/self_hosting_obsidian/)
- [Forked Wordle - removed cooldown - made docker image](https://github.com/Mithun-08/react-wordle)

---

