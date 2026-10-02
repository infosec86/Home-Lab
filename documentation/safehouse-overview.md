# Safehouse Home Lab Overview

Safehouse is a repurposed Debian home server used to build hands-on experience with system administration, cybersecurity, networking, containers, automation, and troubleshooting.

## Hardware

- ASUS E203MA
- 4 GB RAM
- Repurposed as a dedicated always-on lab server

## Operating System

- Debian 13 (Trixie)
- Xfce desktop environment
- Hostname: Safehouse

## Current Technologies

- Linux user and group administration
- OpenSSH remote administration
- Ed25519 SSH keys
- UFW firewall
- Tailscale private networking
- Tailscale exit-node routing
- Nginx
- Docker Engine and Docker Compose
- Glances monitoring
- rsync
- cron
- Linux file permissions
- LXC experimentation
- SELinux experimentation

## Security Approach

The lab is designed to limit unnecessary exposure to the public internet.

Remote administration is performed with SSH over Tailscale. SSH uses public-key authentication, direct root SSH login is disabled, and password-based SSH authentication is disabled.

Services are kept private whenever practical rather than being exposed directly through the home router.

## Purpose

Safehouse provides a controlled environment for practicing Linux administration, networking, cybersecurity concepts, troubleshooting, automation, deployment, and secure remote access while documenting what I learn.
