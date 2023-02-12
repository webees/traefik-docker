# DEMO
```
version: '3.5'
services:
  vaultwarden:
    container_name: vaultwarden
    image: vaultwarden/server
    restart: always
    networks:
      - traefik
    volumes:
      - ./:/data
    environment:
      - DOMAIN=https://pass.dev.run
      - SIGNUPS_ALLOWED=false
      - INVITATIONS_ALLOWED=false
      - SHOW_PASSWORD_HINT=false
      - PASSWORD_HINTS_ALLOWED=false
    labels:
      - traefik.enable=true
      - traefik.http.routers.vaultwarden.entrypoints=https
      - traefik.http.routers.vaultwarden.tls=true
      - traefik.http.routers.vaultwarden.rule=Host(`pass.dev.run`)
      - traefik.http.routers.vaultwarden.service=vaultwarden
      - traefik.http.services.vaultwarden.loadbalancer.server.port=80

networks:
  traefik:
    external: true
```
