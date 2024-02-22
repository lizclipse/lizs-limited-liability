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

### Enhancements

- TODO

### Tweaks

- TODO

### Notes

Some dependency overrides are included because there's some weirdness with mismatched casing
and incomplete metadata.
Each one is tested to make sure it's just a surface-level issue.

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
      # TODO: use a specific tag
      - "PACKWIZ_URL=https://github.com/lizclipse/lizs-limited-liability/raw/master/pack.toml"
      - "VERSION=1.20.1"
      - "MAX_MEMORY=5G"
    volumes:
      # attach the relative directory 'data' to the container's /data path
      - "./volumes/mc/l3:/data:Z"
```

### Dynmap support

For Dynmap to work, the compose will need a couple of additions:

```yml
ports:
  - "8123:8123"
environment:
  # Needed to fix an incompatability with dynmap & quilt
  - "JVM_DD_OPTS=loader.workaround.jar_copy_all_mods=true"
```
