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

          internet                 │                  homelab server (Docker)
                                   │
visitor ──► Cloudflare ◄─── tunnel ─── cloudflared ──► Caddy ─┬─ salem.dev     → site/
                                   │                           └─ app.salem.dev → myapp:8080

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

    /opt/stacks/caddy/
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


### Next Step
- Simple easy configuration for static app.
- Read about Cloudflare tunnel configuration.