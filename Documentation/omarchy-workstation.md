# Omarchy Workstation

Nightfall is the Omarchy/Arch Linux side of the primary lab laptop.

## Current Uses

- Linux command-line practice
- Bash configuration
- Tailscale connectivity
- SSH client access to Safehouse
- QEMU/KVM virtualization
- General cybersecurity tooling

## SSH

Nightfall uses its own Ed25519 key pair to authenticate to Safehouse.

The private key remains on Nightfall and is protected with a passphrase. Only the public key is installed on Safehouse.

## Tailscale

Nightfall can connect directly to Safehouse through Tailscale and can optionally select Safehouse as an exit node when working remotely.

## Virtualization

The workstation includes:

- QEMU
- KVM
- libvirt
- virt-manager
- dnsmasq

These components will support isolated Linux and security-training virtual machines.
