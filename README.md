# alpine-net-debug

A lightweight Alpine-based container image equipped with common networking and debugging tools.

## Shell
- bash

## Included Tools
- curl
- dig (bind-tools)
- ping (iputils)
- netcat-openbsd
- tcpdump
- nmap
- traceroute
- busybox-extras

## Features
- Ready to be attached to any Docker network for debugging.

## Usage

### Build the image
```bash
docker build -t alpine-net-debug:0.0.1 .
```

### Run the container
```bash
docker run -d --name net-debug alpine-net-debug:0.0.1
```

### Enter the container
```bash
docker exec -it net-debug bash
```

When you enter, you'll see the MOTD with usage information.

---

## Using with Docker Compose

Example `docker-compose.yml`:

```yaml
services:
  net-debug:
    image: alpine-net-debug:0.0.1
    container_name: net-debug
    restart: unless-stopped
    tty: true
    stdin_open: true
    command: ["bash","-lc","trap : TERM INT; sleep infinity & wait"]

    networks:
      - debugnet

networks:
  debugnet:
    driver: bridge
    attachable: true
```

Start it with:

```bash
docker compose up -d
docker exec -it net-debug bash
```

---

## Network Debugging

Because the network is **attachable**, you can connect this container to other networks at runtime:

```bash
# attach to another network
docker network connect some_other_net net-debug

# detach from the default network
docker network disconnect debugnet net-debug
```

This allows you to debug traffic between arbitrary containers and networks.

---

## Example MOTD
```
=====================================
Net-Debug Container
Available tools:
bash, curl, dig (bind-tools), ping (iputils),
netcat-openbsd, tcpdump, nmap, traceroute,
busybox-extras
```