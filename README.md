# zfsMiniMonitor
A Docker-based solution for monitor the status of your ZFS zpool and send notifications via Discord webhook.

## How it works?
The script continuously monitors the zpool (based on the `ZPOOL_NAME` variable) at regular intervals (defined by the `CHECK_INTERVAL` variable). \
If it detects a change between checks, it sends the full output via a Discord webhook (using the `WEBHOOK_URL` variable).

## Features
- Runs entirely within a Docker container for simplicity and portability.
- Periodically monitors the status of a specified zpool.
- Sends real-time notifications to Discord when the zpool status changes.
- Provides detailed information about the current zpool state.

## Requirements
- Docker and Docker Compose
- ZFS installed on the host system
- Discord Webhook url

## Docker Compose

```
version: '3.8'
services:
  zfsminimonitor:
    container_name: zfsminimonitor
    image: ghcr.io/zewol95/zfsminimonitor:1.0
    privileged: true
    network_mode: bridge
    environment:
      - ZPOOL_NAME=<YOUR_TANK_NAME>                # Insert here your zpool name
      - WEBHOOK_URL=<YOUR_DISCORD_WEBHOOK_URL>     # Insert here your Discord Webhook url
      - CHECK_INTERVAL=10                          # Time in seconds between checks
    volumes:
      - /dev:/dev
      - /proc:/proc
    restart: unless-stopped

```
