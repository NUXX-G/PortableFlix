# portablelab

Homelab on an old laptop running Ubuntu Server 24.04.

## Stack
- **Docker + Compose** (official repo)
- **Jellyfin** — runs as UID 1000, bound to 127.0.0.1, published only to the tailnet via `tailscale serve` (HTTPS)
- **Tailscale** — remote access and SSH, no ports open to the internet
- **LVM** — separate 250 GB volume for media and transcodes, so a full disk never takes down the OS
- **NFS client** — `/mnt/nas` automount with `nofail`: the server boots even if the NAS is offline

## Layout
    /srv/homelab/<service>/compose.yaml   # versioned
    /srv/homelab/<service>/config|cache   # runtime data, git-ignored
    /srv/media/transcodes                 # Jellyfin temp files (LVM volume)
    /mnt/nas                              # remote library (NFS over Tailscale)

## Run
    cd jellyfin && docker compose up -d
