# OpenTTD — Self-Hosted

Full Transport Tycoon Deluxe in browser + dedicated multiplayer server.
Shut down 2026-03-25 to reduce server load. All config preserved, spin up in ~2 minutes.

## Stack
- **Browser client:** `ghcr.io/rogerrum/docker-openttd` (KasmVNC — full GUI in browser)
- **Game server:** `ghcr.io/ropenttd/openttd` (dedicated server, port 3979)
- **WebSocket bridge:** `jwnmulder/websockify` (lets browser connect to game server)
- **URL:** `https://openttd.playground.montytorr.tech`
- **DNS:** Gandi A record `openttd.playground → 146.190.24.19` (already exists)

## Credentials
- **Browser login:** `cal` / `YOUR_PASSWORD_HERE`
- **Multiplayer server password:** `YOUR_PASSWORD_HERE`
- **Server name:** Cal's OpenTTD Server
- **Max players:** 10

## To bring back up

```bash
cd /root/projects/openttd
docker compose up -d
```

That's it. DNS and Traefik labels are already configured. TLS auto-provisions via Let's Encrypt.

## To shut down again

```bash
cd /root/projects/openttd
docker compose down
# Remove images too (saves ~700MB):
docker rmi ghcr.io/rogerrum/docker-openttd:latest ghcr.io/ropenttd/openttd:latest jwnmulder/websockify:latest
```

## Ports
- `3979/tcp` + `3979/udp` — exposed on host for desktop client connections
- Server registers with OpenTTD coordinator → findable in in-game server browser

## Files
- `docker-compose.yml` — full stack definition
- `config/` — browser client save files / settings (persisted)
- `server-config/openttd.cfg` — dedicated server config
