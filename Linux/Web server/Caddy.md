# Caddy
## Caddy with Docker

## Caddy as a web server and reverse proxy

### Web server vs reverse proxy
Caddy can do two jobs:

- **Web server:** serves files directly (HTML, CSS, images) with `file_server`.
- **Reverse proxy:** receives the request and forwards it to another app
  (e.g. a Java app in a container) with `reverse_proxy`.

### What is a proxy?
A proxy is an intermediary ("middleman") that passes traffic between two sides.

- **Forward proxy:** sits in front of the **users**. The user's traffic goes
  through the proxy, and the proxy connects to the website on their behalf.
  Example: a VPN or a company proxy.
- **Reverse proxy:** sits in front of the **servers**. Visitors connect to the
  proxy, and it decides which app handles the request, based on the domain.
  Example: Caddy, Nginx.

Caddy is a **reverse proxy**:

```text
          internet                 │                  homelab server (Docker)
                                   │
  visitor ──► Cloudflare ◄─── tunnel ─── cloudflared ──► Caddy ─┬─ salem.dev     → site/
                                   │                           └─ app.salem.dev → myapp:8080
```

### Installation
- **With Docker (my setup):** no installation needed. Docker downloads the
  `caddy` image and runs it as a container. The server stays clean and lean,
  and removing it leaves nothing behind.
- **Without Docker:** Caddy can be installed with `apt` and runs as a systemd
  service. Good when the server has no Docker and apps run directly on the OS.

I use the container, because my apps are containers too: Caddy reaches them
by name (`reverse_proxy myapp:8080`) over a shared Docker network, so no ports
need to be published.

### Folder structure

    /opt/stacks/caddy/     # or /srv/
    ├── compose.yml   # which containers run, and how
    ├── Caddyfile     # which domain goes where
    ├── .env          # secrets (tunnel token), never in the repo
    └── site/         # the files visitors see

Each file has one job, so a change in one doesn't touch the others.
Config and content live **outside** the container (mounted with `volumes`),
so deleting or updating the container loses nothing.

### Image vs container
- **Image:** the template (the program, ready but not running). `docker images`
- **Container:** a running copy of the image. `docker ps`

---

## Simple configuration for a static site

Goal: Caddy serves the files in `site/`. No HTTPS yet, no domain yet.
Test it on the server first, then add Cloudflare Tunnel later.

#### 1. Create the folders

```bash
sudo mkdir -p /opt/stacks/caddy/site
cd /opt/stacks/caddy
```

- `/opt`: the Linux directory for external (add-on) apps. It could also be
  `/srv`, where the data the server provides to users lives.
- `/opt/stacks/`: the folder where I collect my stacks (containers).
- `/opt/stacks/caddy/`: the stack for one service, in this case Caddy.

So, `/opt/stacks/caddy` or `/srv/stacks/caddy`?؟



#### 2. `site/index.html`, the page visitors see

```html
<!doctype html>
<html>
  <head><meta charset="utf-8"><title>salem.dev</title></head>
  <body><h1>Hello from my homelab</h1></body>
</html>
```

#### 3. `Caddyfile`, which says what Caddy should do

```caddy
:80 {
    root * /srv
    file_server
}
```

- `:80` means: listen on port 80 for any domain, using plain HTTP.
- `root * /srv` means: the files are in `/srv` inside the container.
  Docker mounts my server folder `/opt/stacks/caddy/site/` (all its files
  and directories) at `/srv` inside the container, using the volume in
  `compose.yml`.
- `file_server` means: send those files to the visitor. This works because
  the files are static. For a Java app, I would use `reverse_proxy` instead.

Why plain HTTP? Later, Cloudflare Tunnel handles HTTPS. If I wrote
`salem.dev` here, Caddy would try to get its own certificate and fail,
because no ports are open to the internet (no exposed ports in my homelab).

#### 4. `compose.yml`, which says how to run the container

```yaml
services:
  caddy:
    image: caddy:2
    container_name: caddy
    restart: unless-stopped
    ports:
      - "127.0.0.1:8080:80"
    volumes:
      - ./Caddyfile:/etc/caddy/Caddyfile:ro
      - ./site:/srv:ro
      - caddy_data:/data
      - caddy_config:/config

volumes:
  caddy_data:
  caddy_config:
```

- `image: caddy:2` uses the official Caddy image, version 2.
- `restart: unless-stopped` starts it again after a crash or reboot.
- `127.0.0.1:8080:80` makes port 80 in the container reachable only
  from the server itself, on port 8080. This is safe because Docker
  bypasses UFW, so I never publish to the whole network.
- `:ro` means read-only. Caddy can read my files but not change them.
- `caddy_data` and `caddy_config` are where Caddy keeps its own state,
  so it survives when the container is recreated.

#### 5. Start it and test it

```bash
sudo docker compose up -d     # start in the background
sudo docker compose ps        # should show "running"
curl http://127.0.0.1:8080    # should print my HTML
sudo docker compose logs caddy   # if something is wrong
```




### Next Step
- Read about Cloudflare tunnel configuration.