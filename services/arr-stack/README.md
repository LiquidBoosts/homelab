# Arr Stack (Radarr, Sonarr, Prowlarr, qBittorrent)

## Overview

The Arr stack manages automated media downloading and sorting. It connects indexers to download clients and renames/sorts media into the Jellyfin library.

### Services Included:
- **Radarr** – Movies
- **Sonarr** – TV Shows
- **Prowlarr** – Indexer Aggregator
- **qBittorrent** – Torrent Client

## VM Specs
### Docker VM
- **OS:** Ubuntu 24.04.2 LTS
- **RAM:** 12GB
- **CPU:** 6 Cores
- **Storage:** 64GB SSD
- **IP Address**: `192.168.8.208`

> Media and torrent directories are mounted into the VM via NFS from the Proxmox host (`/mnt/tank`).  
> The local SSD is used for Docker configs and app databases.


## Folder Layout

```bash
/mnt/tank
└── arr
    ├── media
    │   ├── books
    │   ├── movies
    │   ├── music
    │   └── tv
    └── torrents
        ├── books
        ├── movies
        ├── music
        └── tv
```
```bash
/opt/arr
├── compose.yml
├── jellyfin
├── jfago
├── plex
├── prowlarr
├── qbittorrent
├── radarr
└── sonarr
```






## Setup Access with Domain Names (Dynamic IP)

To make sure your domain stays updated with your home IP, install and configure `ddclient` on your reverse proxy container:  
`sudo apt install ddclient -y`

Edit `/etc/ddclient.conf` :
```bash
protocol=cloudflare
ssl=yes
zone=domain.com
ttl=1
use=web, web=ipify-ipv4
login=token
password='${CLOUDFLARE_API_TOKEN}'

jellyfin.domain.com
accounts.domain.com
```
Zone = your root domain on cloudflare. (e.g. domain.com)  
Password = your cloudflare api token.  
List your subdomains on separate lines for each service (e.g. jellyfin.domain.com, accounts.domain.com)  

### Add Services to Ngix Proxy Manager  
For each subdomain (e.g. accounts.domain.com)  
Go to NPM → Hosts → Proxy Hosts → Add Proxy Host  
Domain name: `accounts.domain.com`  
Forward Hostname/IP: The IP of the VM.  
Forward Port: The port of the service. (e.g. Jellyfin = 8096)  
Enable websocket support and block common exploits  
Add SSL via Let's Encrypt tab.  
