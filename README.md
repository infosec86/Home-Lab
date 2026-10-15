# Home Lab

This repository is my running record of building a home lab from hardware I already had or could get cheaply. I am using it to get more comfortable with Linux, networking, cybersecurity, virtualization, containers, remote administration, and troubleshooting.

I want this repo to be more than anything my online journal of my journey through networks and security. So far, a lot of the useful parts have come from getting something wrong, checking what the system is actually doing, and then understanding why the fix worked. That is what I want to document here.

The lab is also intentionally budget-focused. I would rather learn how to get useful work out of an old 4 GB laptop and a used corporate mini PC than spend a lot of money on finished hardware and skip the parts I actually want to learn. Over time, the equipment will improve as I fully understand what it is I'm using and what I want to achieve. It's easy to spend a lot on equipment that I may not use fully.

## What I am building

Right now the lab has three main pieces.

### Safehouse — Debian server

Safehouse is an ASUS E203MA with 4 GB of RAM that I repurposed as a small Debian 13 server. It is not powerful, which has actually made it a good machine to learn on because I have to pay attention to what I install and what is running.

I currently use it for:

- Debian 13 / Xfce
- SSH administration with Ed25519 keys
- Tailscale private networking
- Tailscale exit-node routing
- UFW
- Nginx
- Docker and Docker Compose
- Glances
- btop
- tmux
- rsync and cron practice
- Linux permissions and user management
- LXC experiments
- service management with systemd
- basic Python practice

One example of why I keep this repo is Glances. I saw Glances report that it was listening on `0.0.0.0:61208` and initially thought I had exposed it more broadly than I wanted. After checking Docker with `docker ps`, I found that the container was listening on all interfaces internally, but Docker was only publishing it to `127.0.0.1:61208` on Safehouse. Tailscale Serve then provides the remote path to that local service. That helped me understand the difference between what an application is listening on inside a container and what the host is actually exposing.

I have also been using `btop` a lot more lately instead of always opening the Glances web interface. Glances is still useful, but `btop` is a really quick way to check CPU, memory, processes, and general system health when I am already in the terminal.

### Nightfall — Omarchy / Arch Linux

Nightfall is the Omarchy side of my Acer laptop. I use it when I want to work in Linux natively instead of inside a VM.

I am using it for Linux command-line practice, SSH, Tailscale, Wireshark/tshark, virtualization with QEMU/KVM and virt-manager, and eventually isolated security-training VMs.

It also has simple `safehouse-on` and `safehouse-off` shortcuts so I can choose Safehouse as a Tailscale exit node without typing the full command every time.

### Windows workstation

The same Acer also runs Windows 11 and is my main everyday/control system.

Current lab use includes:

- VMware Workstation
- Xubuntu VM
- Windows administration
- Tailscale
- PowerShell
- remote administration of Safehouse
- cross-platform troubleshooting between Windows and Linux

The Xubuntu VM currently runs with 3 GB RAM, 2 CPU cores, NAT networking, a growable virtual disk, and LUKS/LVM encryption. The Acer only has about 8 GB of soldered RAM, so I am learning to work within that limit instead of pretending it is a large virtualization host.

I also created PowerShell functions named `safehouse-on` and `safehouse-off`. I originally mixed up which machine was supposed to be the exit node. The command runs on HomeLaptop, but it points to Safehouse because Safehouse is the machine providing the exit route. Once that clicked, the setup made a lot more sense.

### Phone access while traveling

I have also added Tailscale to my personal phone so I can check on the home lab even when I am traveling and do not have my laptop with me.

I installed Termux on the phone and use a small Bluetooth keyboard and mouse that are portable enough to fit in my pocket. I am not using this setup every day, but it is nice knowing I can reach Safehouse, check status, or do something simple from almost anywhere if I need to.

## How I am approaching security

I am trying to keep services private unless I have a reason to expose them.

For example, SSH uses keys instead of passwords, direct root SSH login is disabled, and Safehouse is normally reached through Tailscale rather than by forwarding SSH through the home router. Glances is bound to localhost on the host side and reached remotely through Tailscale Serve.

I am also learning that security is not just a checklist. A control can be technically secure and still be annoying enough that somebody works around it. Part of the lab is learning how to make remote access convenient while still limiting exposure.

This public repository does not contain private keys, passwords, tokens, live VPN configuration files, or other secrets.

## Documentation

- [Safehouse Overview](Documentation/safehouse-overview.md)
- [SSH Hardening](Documentation/ssh-hardening.md)
- [Tailscale Remote Access and Exit Node](Documentation/tailscale-remote-access.md)
- [Omarchy Workstation](Documentation/omarchy-workstation.md)
- [Virtualization Lab](Documentation/virtualization.md)
- [VMware Network Incident](Documentation/network-incident-vmware-connectivity.md)
- [Lessons Learned](Documentation/lessons-learned.md)

## What I want this repo to show

I am not trying to make the lab look more advanced than it is. I want to understand how the pieces connect, notice when something is wrong, troubleshoot it, and explain what I learned.

That means I am going to keep notes about mistakes and confusion instead of cleaning all of that out afterward. If I thought `ifconfig` was its own package and then learned it comes from `net-tools`, that is worth recording. If I thought a Tailscale command belonged on Safehouse when it really belonged on the client, that is worth recording too.

Those small moments are where a lot of the learning is happening and may help others who are just starting out. All the learning I did in academics was priceless, but I've remembered much more by physically doing it. I will say, however, that all those notes I took in class came in very handy, so a personal pat on my back for that one.

## Current hardware direction

I am keeping the Acer as my main laptop/control station and keeping Safehouse as the lightweight Debian server.

Rather than buying several laptops, the next major hardware step is likely one inexpensive used corporate mini PC with replaceable DDR4 memory. Machines such as ThinkCentre Tiny, OptiPlex Micro, and EliteDesk Mini systems are interesting because they are small, low-power, easy to find used, and can often be upgraded to 32 GB or more.

The goal is to turn one of those into the first dedicated Proxmox host and move the heavier VM workload off the Acer.

The basic direction is: Acer / control laptop -> LAN or Tailscale -> managed switch -> Safehouse for Debian/Docker services and a Proxmox mini PC for Kali, Windows Server, Windows clients, Linux servers, and other lab systems.

I am not buying three Proxmox nodes just to say I have a cluster. I want to start with one host, learn what actually limits me, and add hardware when there is a reason for it.

## Things I want to build toward

One of my next smaller projects is automating Safehouse security updates so I do not have to keep logging in just to install routine packages and updates. I am thinking about having it check and apply the appropriate updates on a schedule, possibly every three days, while still keeping enough visibility to know what changed and whether a reboot is needed.

Over time I want to work with Windows Server and Active Directory, VLANs, managed switches, firewall/router labs, SIEM and logging, vulnerable training machines, network segmentation, shared storage, backups, Proxmox clustering concepts, and eventually some AI/programming projects.

I also want to build a small physical rack or shelf setup eventually, but the equipment matters more than the rack. RAM, storage, networking, and useful compute come before making it look impressive.

The main goal is simple: keep building the lab one piece at a time and understand why each piece is there.
