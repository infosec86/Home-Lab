# Virtualization Lab

Virtualization is where the lab starts to get more interesting for me because it lets me build systems that would be expensive or inconvenient to run as separate physical machines.

I am also trying not to turn this into a competition to see how many VMs I can run at once. My Acer only has about 8 GB of soldered RAM, so right now virtualization is as much about learning resource limits as it is about spinning up machines.

## What I am using now

On Windows I have VMware Workstation running an Xubuntu VM.

That VM currently has roughly:

- 2 vCPU
- 3 GB RAM
- 40 GB growable disk
- NAT networking
- LUKS/LVM encryption

On Omarchy I installed QEMU/KVM, libvirt, virt-manager, and dnsmasq so I can learn Linux-native virtualization too.

## What I want to run

### Kali Linux

I want a dedicated Kali VM for authorized lab work, HTB practice, packet analysis, enumeration, and learning security tools without turning my everyday operating system into a pile of testing software.

A lightweight starting point is enough:

- 2 vCPU
- 2 GB RAM
- 30-40 GB virtual disk

### Vulnerable targets

I want intentionally vulnerable systems such as Metasploitable or vulnerable web applications, but I do not want them bridged casually onto the household LAN.

The goal is to build a network where the attacker VM and target VM can talk to each other without unnecessarily exposing everything else in the house.

### General Linux servers

I also want plain Debian or Ubuntu server VMs because not every useful exercise needs to involve exploitation.

Those can be used for SSH, firewall rules, logging, permissions, services, web servers, troubleshooting, and hardening.

### Windows Server and clients

Longer term I want Windows Server, Active Directory, and Windows clients so I can practice domains, users, groups, Group Policy, DNS, and administration in a small environment I actually control.

## Networking is the part I want to understand, not hide

One thing I am trying to avoid is clicking through VM network settings without knowing what they mean.

NAT, bridged networking, host-only networks, isolated networks, and eventually VLANs all change who can talk to whom.

For vulnerable systems, I want the network design to be deliberate. If a target only needs to communicate with Kali, I should not give it access to the rest of my household network just because bridged mode is easy.

## Why I am planning a Proxmox host

The Acer is fine for learning, but 8 GB of RAM becomes the real bottleneck very quickly.

Instead of replacing the Acer, I want to keep it as my control laptop and eventually buy one inexpensive corporate mini PC with replaceable DDR4 memory. That machine can become a dedicated Proxmox host with 16 GB or 32 GB to start, then grow later if needed.

The basic direction is: Acer -> Proxmox host -> Kali, Windows Server, Windows client, Linux server, and other lab systems.

I am deliberately starting with one host instead of buying a cluster immediately. I want to learn what one system can do, what actually becomes a limitation, and then add hardware for a reason.

## What I am learning from virtualization already

The biggest lesson so far is that virtualization adds another layer that can fail independently of the physical machine.

When my Xubuntu VM lost network connectivity but Windows stayed online, that forced me to think about the guest NIC, VMware NAT, routes, DNS, and the host separately.

That was more useful than simply knowing how to create a VM because it made me troubleshoot the virtual infrastructure itself.
