# Safehouse Home Lab Overview

Safehouse is my personal Linux home lab built to develop hands-on experience with system administration, cybersecurity, networking, containers, automation, and troubleshooting.

## Hardware

• ASUS E203MA
• 4 GB RAM
• Repurposed as a dedicated home lab server

## Operating System

• Debian 13 (Trixie)
• Xfce desktop environment
• Hostname: Safehouse

## Current Technologies

• Linux user and group administration
• SSH remote administration
• Ed25519 SSH keys
• UFW firewall
• Tailscale private networking
• Nginx web server
• Docker Engine
• Docker Compose
• Glances system monitoring
• rsync
• cron
• Linux file permissions
• LXC container experimentation
• SELinux experimentation

## Security Approach

The lab is designed around limiting unnecessary exposure to the public Internet.

Remote admin is performed via tailscale & SSH password authentication. Root SSH access have been disabled. Services are kept private whenever possible rather than being directly exposed to the Internet.

## Purpose

The purpose of 'Safehouse' is to provide a controlled environment where I can practice Linux administration, cybersecurity concepts, networking, troubleshooting, automation, and deployment while documenting what I learn.
