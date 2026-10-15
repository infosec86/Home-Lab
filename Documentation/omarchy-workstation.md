# Omarchy Workstation

Nightfall is the Omarchy/Arch Linux side of my Acer laptop. I use it when I want to work in Linux directly instead of through a VM.

I am still getting comfortable with Arch-style tooling and the way Omarchy is put together, so this machine is partly a workstation and partly another learning environment.

## What I use it for

So far I have used Nightfall for:

- Linux command-line practice
- Bash configuration
- Tailscale
- SSH access to Safehouse
- Wireshark / tshark work
- QEMU/KVM
- libvirt and virt-manager
- general security tooling
- planning isolated Kali and vulnerable lab VMs

## SSH to Safehouse

Nightfall has its own Ed25519 key pair for connecting to Safehouse.

The private key stays on Nightfall and is protected with a passphrase. Only the public key is copied to Safehouse.

One thing that keeps coming up is remembering which side of an SSH connection I am working on. The client has the private key and starts the connection. Safehouse has the matching public key in `authorized_keys` and decides whether to accept it.

That sounds simple, but keeping the client/server roles straight has saved me from changing the wrong machine more than once.

## Tailscale and Safehouse

Nightfall can reach Safehouse directly over Tailscale without exposing SSH through the home router.

I also added shortcuts so I can turn Safehouse into the internet exit point for Nightfall when I want to:

```bash
safehouse-on
safehouse-off
```

The shortcut itself is not the important part. What finally clicked for me was that Nightfall is the client choosing an exit node, while Safehouse is the system advertising that it can be one.

## Virtualization

I installed:

- QEMU
- KVM
- libvirt
- virt-manager
- dnsmasq

The original idea was to use Nightfall for Kali and other security VMs. I still plan to do that, but the Acer's 8 GB of soldered RAM is a real limit. That is one of the reasons I am now planning a separate used mini PC as a future Proxmox host instead of trying to force the Acer to run everything.

For now, Nightfall is still useful for learning how Linux virtualization works and how it differs from VMware on Windows.
