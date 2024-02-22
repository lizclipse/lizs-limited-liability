# Liz's Limited Liability

A modpack with the intent to extend and enhance instead of overhaul.

most of this is TODO

## Goals

- Lightweight
  - Number of mods is less important than size
- Steam Deck compatability & controller support
  - I want to play this on the sofa and with a controller sue me

## Mod Overview

### Gameplay

- TODO

### Tweaks

- TODO

## Server

Compose definition:

```yml
version: "3.8"

services:
  mc:
    image: docker.io/itzg/minecraft-server
    tty: true
    stdin_open: true
    ports:
      # Server
      - "25565:25565"
      # Voice chat
      - "24454:24454"
    environment:
      - "EULA=true"
      - "TYPE=quilt"
      - "PACKWIZ_URL=http://192.168.0.200:8000/pack.toml"
      - "VERSION=1.20.1"
      - "MAX_MEMORY=5G"
    volumes:
      # attach the relative directory 'data' to the container's /data path
      - "./volumes/mc/l3:/data:Z"
```

### Dynmap support

Env:

```yml
environment:
  # Needed to fix an incompatability with dynmap & quilt
  - JVM_DD_OPTS=loader.workaround.jar_copy_all_mods=true
```

Port:

```yml
ports:
  - "8123:8123"
```
