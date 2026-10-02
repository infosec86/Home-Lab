# Tailscale Remote Access and Exit Node

## Objective

Tailscale is used to provide secure remote access to the home lab without forwarding administrative ports through the home router.

## Remote Access

Safehouse and authorized client systems are members of the same private Tailscale network.

SSH runs over that private connection:

```text
Remote client
     |
     | encrypted Tailscale connection
     v
Safehouse
     |
     +-- SSH
     +-- private services
```

## Exit Node

Safehouse is also configured as a Tailscale exit node for testing trusted remote browsing from networks such as hotels or public Wi-Fi.

When enabled on a client:

```text
Remote client
     |
     | Tailscale
     v
Safehouse
     |
     v
Internet
```

This is a networking and secure-remote-access exercise. It does not make the client anonymous; internet traffic still exits through the home internet connection unless another upstream VPN is deliberately configured.

## Linux Client Shortcuts

The Omarchy client uses Bash aliases so the exit node can be enabled and disabled without remembering the full command:

```bash
alias safehouse-on='sudo tailscale set --exit-node=<SAFEHOUSE_TAILSCALE_IP>'
alias safehouse-off='sudo tailscale set --exit-node='
```

The live Tailscale address is intentionally not stored in this repository.

## Testing

The configuration has been tested by:

- Reaching Safehouse over Tailscale
- Using SSH through the tailnet
- Confirming connectivity after reboot
- Accessing the server while its laptop lid is closed
- Selecting Safehouse as an exit node
- Confirming the client route changes when the exit node is enabled and disabled

## What I Learned

This project has provided hands-on practice with overlay networking, encrypted remote access, exit-node routing, client/server roles, and troubleshooting the difference between connectivity problems and authentication problems.
