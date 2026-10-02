# Home Lab

This repository documents my personal home lab and the hands-on work I am doing to build practical experience with Linux, networking, cybersecurity, virtualization, containers, remote administration, and troubleshooting.

The lab is intentionally built from repurposed and existing hardware so I can learn how the pieces work rather than simply buying a finished solution.

I am still early in the hands-on portion of this work, so the repository is meant to show the learning process as much as the finished result. I am documenting what I try, what works, what fails, how I troubleshoot it, and what I learn along the way. The goal is not to make the lab look more advanced than it is. I want it to reflect steady, practical growth in systems administration and cybersecurity.

## Current Lab

### Safehouse — Debian Home Server

Safehouse is a repurposed ASUS laptop running Debian 13 and acting as the always-on server component of the lab. It is intentionally modest hardware, which makes it useful for learning how to work within real resource constraints.

Current work on Safehouse includes:

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

Safehouse is being used to learn Linux administration, service management, remote access, networking, containerization, monitoring, permissions, and troubleshooting.

### Nightfall — Omarchy / Arch Linux Workstation

Nightfall is the Omarchy/Arch Linux side of the primary lab laptop. It is used as a Linux workstation and as a platform for expanding into virtualization and security lab work.

Current and planned work includes:

- Linux command-line practice
- Bash configuration
- Tailscale client connectivity
- SSH client access to Safehouse
- QEMU/KVM virtualization
- libvirt and virt-manager
- Planned Kali Linux deployment
- Planned isolated security-training VMs
- Networking and routing experiments

### Windows Workstation

The same primary laptop also provides a Windows environment for Windows administration and VMware-based virtualization.

Current work includes:

- VMware Workstation
- Xubuntu VM
- Windows administration
- Virtualization practice
- Cross-platform troubleshooting between Windows and Linux systems

## Security Approach

The lab focuses on defensive configuration and learning how to reduce unnecessary exposure while still keeping systems useful.

Examples include key-based SSH authentication, disabling direct root SSH access, limiting public-facing services, using private overlay networking, isolating intentionally vulnerable training systems, and documenting troubleshooting steps.

The lab is also being used to understand how security controls affect usability. For example, remote access should remain convenient enough to use while still requiring deliberate authentication, and intentionally vulnerable systems should be reachable for training without being unnecessarily exposed to the household network.

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
- Learn how services, networks, operating systems, and virtualization interact
- Document real troubleshooting and configuration work
- Build a portfolio of hands-on projects that demonstrates technical ability
- Develop enough practical experience to explain not only what I configured, but why it works and how I would troubleshoot it

## Learning Style

This repository intentionally keeps scripts and command examples simple.

I am still building confidence with Bash, Linux administration, networking, virtualization, and automation. When code or shell commands are included, I prefer short examples that I can understand line by line rather than large scripts that hide what is happening.

As the lab grows, some automation will become more advanced, but the documentation will continue to explain the purpose of the commands and the reasoning behind the configuration.

## Next Steps

Planned additions include Kali Linux, intentionally vulnerable training targets, additional network segmentation, firewall/router labs, VPN routing experiments, and a gradual expansion of the physical lab.

The next hardware phase will focus on adding inexpensive, upgradeable equipment rather than replacing the lab with a single high-cost system. A used ThinkPad may serve as the next step because it can provide more RAM, additional SSD capacity, and more room for virtualization while remaining inexpensive and easy to upgrade.

The ThinkPad would not necessarily be the permanent center of the lab. It would be another step toward a more capable environment while I learn what hardware resources actually matter for the workloads I am building.

Longer term, I want to move toward a compact desktop server-rack style setup that can sit on or near a desk. The goal is not to build a large enterprise-style rack, but to create a small physical environment where I can work with the same types of components found in larger infrastructure.

Planned hardware additions include:

- Managed or lab-focused Ethernet switches
- Additional SSD storage
- Removable storage and other media for backup and recovery practice
- RAM upgrades
- Small form factor PCs or mini PCs
- Dedicated storage nodes
- Dedicated virtualization or compute nodes
- Network adapters and additional interfaces for segmentation experiments
- A compact rack, shelf, or enclosure to organize networking, storage, and compute hardware

As hardware is added, I want to use it for practical exercises such as:

- Installing and replacing SSDs
- Expanding RAM
- Managing disks, partitions, and filesystems
- Building backup and recovery workflows
- Creating multiple virtual networks
- Configuring VLANs and managed switches
- Separating trusted, lab, and intentionally vulnerable systems
- Running multiple VMs at the same time
- Monitoring hardware and network resources
- Testing firewall and routing rules
- Practicing system recovery after configuration mistakes or hardware changes

The goal is to build the environment incrementally so each addition becomes another learning project rather than simply adding equipment for the sake of having more hardware.
