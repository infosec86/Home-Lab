# Home Lab

This repository documents my personal home lab and the hands-on work I am doing to build practical experience with Linux, networking, cybersecurity, virtualization, containers, remote administration, and troubleshooting.

The lab is intentionally built from repurposed and existing hardware so I can learn how the pieces work rather than simply buying a finished solution.

## Current Lab

### Safehouse — Debian Home Server

- Debian 13
- SSH key-based remote administration
- Tailscale private networking
- Tailscale exit-node testing
- UFW firewall
- Nginx
- Docker and Docker Compose
- Glances monitoring
- rsync and cron practice
- Linux permissions and user management
- LXC experimentation
- SELinux experimentation

### Nightfall — Omarchy / Arch Linux Workstation

- Linux command-line practice
- Tailscale client
- SSH client access to Safehouse
- QEMU/KVM virtualization
- libvirt and virt-manager
- Planned Kali Linux and isolated security-training VMs

### Windows Workstation

- VMware Workstation
- Xubuntu VM
- Windows administration and virtualization practice

## Security Approach

The lab focuses on defensive configuration and learning how to reduce unnecessary exposure while still keeping systems useful.

Examples include key-based SSH authentication, disabling direct root SSH access, limiting public-facing services, using private overlay networking, isolating intentionally vulnerable training systems, and documenting troubleshooting steps.

This repository does not contain private keys, credentials, access tokens, live VPN configuration files, or other secrets.

## Documentation

- [Safehouse Overview](documentation/safehouse-overview.md)
- [SSH Hardening](Documentation/ssh-hardening.md)
- [Tailscale Remote Access and Exit Node](Documentation/tailscale-remote-access.md)
- [Omarchy Workstation](Documentation/omarchy-workstation.md)
- [Virtualization Lab](Documentation/virtualization.md)
- [Lessons Learned](Documentation/lessons-learned.md)

## Goals

The purpose of this lab is to:

- Build practical IT and cybersecurity skills
- Develop Linux and networking confidence
- Practice secure system administration
- Create isolated environments for authorized security testing
- Document real troubleshooting and configuration work
- Build a portfolio of hands-on projects that demonstrates technical ability

## Future Lab Work

Planned additions include Kali Linux, intentionally vulnerable training targets, additional network segmentation, firewall/router labs, VPN routing experiments, and eventually more capable dedicated lab hardware.
