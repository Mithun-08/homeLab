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

[BuyLink (For India)](https://nationalpc.in/pre-built-mini-pc/asus-nuc14-essential-kit-nuc14mnk-b-n150-processor-16gb-ddr5-laptop-ram-128gb-m-2-nvme-ssd-windows-11pro)

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
- [Setting up piHole in Airtel GPON Router if you can get admin access](https://medium.com/@rishikeshu/pihole-on-airtel-g-2425g-a-modem-fb716ece2ea3)
- [Forked Wordle - removed cooldown - made docker image](https://github.com/Mithun-08/react-wordle)
- [Setting up Postfix](https://www.youtube.com/watch?v=uNss377DK88&t=426s&pp=ygUScG9zdGZpeCBob21lc2VydmVy)

---

## Learned the Hard Way

**Proxmox vs Ubuntu Server**
Started setting up Proxmox but found out halfway through that it 
cannot recognise the Intel N150's integrated GPU. Since I needed GPU 
hardware acceleration for media transcoding, I switched to Ubuntu Server.

**Own Domain vs Tailscale**
Having your own domain makes it much easier to publicly access and 
navigate your services. Without a domain you can still access services 
from anywhere using Tailscale's Magic DNS, but the client device needs 
to stay connected to the Tailscale network.

**Indian ISPs and CGNAT**
Indian ISPs are behind CGNAT, meaning your router doesn't have its own 
public IP — so you can't expose ports to host services publicly. This 
is where Cloudflare Tunnel comes in. It creates a secure tunnel between 
your server and Cloudflare without exposing any ports, letting you 
access your services from anywhere.

**Pihole + Airtel**
Hosting Pihole is effectively useless with Airtel as your ISP. Most 
router settings are greyed out and customer support was no help. Without 
the ability to change the DNS provider to Pihole, you have to manually 
point each device to use it as its DNS — which defeats the purpose.

**Nextcloud + OnlyOffice**
Just running Nextcloud isn't enough. Without an office suite you still 
have to download, edit and re-upload documents. OnlyOffice lets you open 
and save files directly in the browser — no hassle.

---

