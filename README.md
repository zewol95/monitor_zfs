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
services:
  zfs_monitor:
    container_name: zfs-monitor
    image: zfs-monitor
    privileged: true
    network_mode: bridge
    environment:
      - ZPOOL_NAME=<name_of_zpool>                       # ENTER HERE YOUR ZPOOL NAME
      - WEBHOOK_URL=<web_url_of_your_Discord_Webhook>    # ENTER HERE YOUR WEBHOOK URL
      - CHECK_INTERVAL=60                                # ENTER HERE THE TIME BETWEEN CHECKS (SUGGESTED 60s)
    volumes:
      - /dev:/dev
      - /proc:/proc
    restart: unless-stopped
```

jjj
