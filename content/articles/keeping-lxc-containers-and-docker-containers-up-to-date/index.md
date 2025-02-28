+++
author = "Tom Claessens"
title = "Keeping LXC containers with docker containers up-to-date"
date = "2025-02-28"
description = "How to automatically update Ubuntu LXC containers with unattended-upgrades and keep Docker containers up-to-date using Watchtower for better security"
tags = ["technology"]
showtoc = false
TocSide = "right"
+++
When running Ubuntu inside an LXC container, it's important to keep the system up-to-date with security patches and updates. Additionally, if you are running Docker containers inside your LXC environment, those need regular updates as well. This guide covers automating updates using `unattended-upgrades` for the LXC container and `watchtower` for Docker containers.

## 1. Keeping Ubuntu Updated with Unattended-Upgrades

### Installing Unattended-Upgrades

First, ensure that `unattended-upgrades` is installed on your LXC container:

```shell
sudo apt update && sudo apt upgrade -y
sudo apt install unattended-upgrades -y
```

## Configuring Unattended-Upgrades

Edit the configuration file at `/etc/apt/apt.conf.d/50unattended-upgrades`:

```shell
sudo vi /etc/apt/apt.conf.d/50unattended-upgrades
```
Ensure the following settings are enabled:

```shell
Unattended-Upgrade::Allowed-Origins {
    "${distro_id}:${distro_codename}-security";
    "${distro_id}:${distro_codename}-updates";
};
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "02:00";
```

This configuration ensures security and general updates are installed automatically and the system reboots if necessary at 2 AM.

### Enabling Unattended-Upgrades

Enable the service to run automatically:

```shell
sudo systemctl start unattended-upgrades
sudo systemctl enable unattended-upgrades
```

This command enables automatic updates.

### Running Unattended-Upgrades on a Schedule

To run updates at specific intervals, add a cron job:

```shell
sudo crontab -e
```

Add the following line at the end of the file to run updates every day at midnight:

```shell
0 0 * * * /usr/bin/unattended-upgrade -d
```

## 2. Keeping Docker Containers Updated with Watchtower

Watchtower is a Docker container that automatically updates running containers when new images become available.

If you are using Docker Compose, add the following to your `docker-compose.yml`:

```yaml
services:
  watchtower:
    image: containrrr/watchtower
    container_name: watchtower
    restart: unless-stopped
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    command: --schedule "0 0 * * *"
```

This configuration:

- Uses the official `containrrr/watchtower` image
- Mounts the Docker socket to manage containers
- Runs Watchtower daily at midnight to check for updates

### Running Watchtower

Deploy Watchtower with:

```shell
docker compose up -d
```

## Conclusion

By setting up `unattended-upgrades` and `watchtower`, your LXC containers and Docker workloads will always stay updated, reducing security risks and ensuring you’re running the latest versions of your software automatically.