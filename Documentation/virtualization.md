# Virtualization Lab

Virtualization is being added to the home lab so security exercises can run in isolated environments without placing intentionally vulnerable services directly on the household network.

## Current Platforms

### Windows Host

VMware Workstation currently hosts an Xubuntu VM.

### Omarchy Host

The Omarchy workstation uses QEMU/KVM, libvirt, virt-manager, and dnsmasq.

## Planned Virtual Machines

### Kali Linux

A dedicated penetration-testing workstation for authorized lab exercises.

Initial lightweight target configuration:

- 2 vCPU
- 2 GB RAM
- 30–40 GB virtual disk

### Metasploitable 2

An intentionally vulnerable Linux target for practicing scanning, enumeration, and exploitation inside an isolated lab network.

### Debian or Ubuntu Server

A general server target for practicing:

- SSH configuration
- Firewall rules
- Hardening
- Logging
- Web services
- Permissions
- Troubleshooting

### Web Security Targets

Applications such as OWASP Juice Shop and DVWA may be deployed in containers rather than full VMs.

## Network Design

Intentionally vulnerable systems should use isolated or carefully controlled virtual networks rather than being bridged directly onto the household LAN.

The goal is to allow attacker and target systems to communicate while limiting unnecessary access to other devices.

## Future Expansion

With additional RAM and hardware, the lab may later include:

- Windows Server
- Active Directory
- pfSense or OPNsense
- Security Onion
- Multiple subnets and firewall zones
