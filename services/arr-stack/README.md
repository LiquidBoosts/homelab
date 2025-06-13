# Arr Stack (Radarr, Sonarr, Prowlarr, qBittorrent)

## Overview

The Arr stack manages automated media downloading and sorting. It connects indexers to download clients and renames/sorts media into the Jellyfin library.

### Services Included
- **Radarr** – Movies
- **Sonarr** – TV Shows
- **Prowlarr** – Indexer Aggregator
- **qBittorrent** – Torrent Client

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
