# caddy-cloudflare-docker

Docker container for Caddy with built in Cloudflare for DNS validation

### Docker Compose

```yaml
---
version: "3.4"
services:
  caddy:
    image: ghcr.io/deanpcmad/caddy-cloudflare-docker:main
    container_name: caddy
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    extra_hosts:
      - "host.docker.internal:host-gateway"
    volumes:
      - ./data/caddy/Caddyfile:/etc/caddy/Caddyfile
      - ./data/caddy/data:/data
```

### Caddyfile

```
mydomain.com {
  reverse_proxy container:3000
  tls {
    dns cloudflare TOKEN
  }
}

```
