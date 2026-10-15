# Safehouse

Safehouse is the first physical server in my home lab. It is an old ASUS E203MA with 4 GB of RAM running Debian 13.

I kept the hardware on purpose. It would have been easy to say the laptop is too weak and buy something better, but working with a limited machine has forced me to think about what services actually need, what should run in Docker, what can stay lightweight, and when an upgrade is actually justified.

## What is running on it

Right now Safehouse is used for:

- Debian 13 (Trixie)
- Xfce
- OpenSSH
- Ed25519 key authentication
- Tailscale
- Tailscale exit-node routing
- UFW
- Nginx
- Docker Engine and Docker Compose
- Glances
- tmux
- rsync
- cron
- Linux user/group and permission practice
- LXC experiments
- systemd service management
- basic Python practice

## How I normally manage it

Most of the time I do not sit at Safehouse directly. I connect from my Acer over Tailscale and administer it through SSH.

That has been useful because it makes even a small home server feel more like a real remote system. If I break networking or SSH, I have to think about the fact that I may also break my own management path.

I use key-based SSH authentication, password SSH login is disabled, and direct root SSH login is disabled. I connect as a normal user and use `sudo` only when I need elevated privileges.

## Glances and Docker

Glances is running in Docker and gives me a web view of CPU, memory, disk, processes, and network activity.

One of the more useful things I learned came from a warning that Glances was listening on:

```text
0.0.0.0:61208
```

At first I thought that meant I had exposed Glances on every Safehouse interface.

After checking Docker, I found the host-side mapping was actually:

```text
127.0.0.1:61208->61208/tcp
```

So Glances was listening broadly inside the container, while Docker only published it to localhost on the host. Tailscale Serve then forwards the private tailnet connection to that local port.

That was a good example of why I want to document the lab this way. The final configuration matters, but understanding why that output was not as dangerous as I first thought mattered more.

## Tailscale and travel use

Safehouse also advertises itself as a Tailscale exit node.

From Windows or Omarchy on my Acer I can leave normal internet traffic alone and only use Tailscale to reach Safehouse, or I can enable the exit node and route internet traffic through my home connection.

The part that confused me initially was that the exit-node selection command runs on the client, not on Safehouse. Safehouse advertises the capability; the Acer chooses whether to use it.

That distinction is simple now, but it took actually testing it and watching `tailscale status` change before it really stuck.

## Things that surprised me

I expected some older Linux commands to just be there. For example, `ifconfig` was not installed, and I initially looked for a package named `ifconfig`. I learned that it comes from `net-tools`, while modern Debian expects commands such as `ip addr` or `ip a`.

I also started using tmux more than I expected. Keeping a normal shell, Docker view, and service logs open at the same time makes troubleshooting much easier than constantly reconnecting or opening separate windows.

## Why Safehouse still matters

Safehouse is not meant to become a giant virtualization server. It only has 4 GB of RAM and that is fine.

Its role is becoming clearer as the lab grows: lightweight Linux services, Docker experiments, remote administration, networking, monitoring, automation, and a machine I can afford to break while learning how to fix it.

Heavier virtualization will eventually move to a dedicated Proxmox mini PC, but I plan to keep Safehouse as a separate physical Linux server in the environment.
