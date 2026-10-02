# Lessons Learned

This document records practical troubleshooting and design lessons from building the home lab.

## Know Which Machine You Are On

Many networking tasks involve both a client and a server. Before running a command, confirm whether it belongs on:

- Safehouse — Debian server
- Nightfall — Omarchy workstation
- Windows workstation

This avoids accidentally applying a client-side command to the server or vice versa.

## Connection Timeout vs. Authentication Failure

These errors mean very different things:

```text
Connection timed out
```

usually points toward connectivity, routing, firewall, or service availability.

```text
Permission denied (publickey)
```

means the SSH server was reached, but authentication failed.

## Use Verbose SSH Output

`ssh -vvv` shows which keys the client attempts and helps identify whether a problem is on the network side or the authentication side.

## Wi-Fi Power Management

Safehouse is a laptop used as an always-on server. Its active NetworkManager profile was configured with Wi-Fi power saving disabled so network availability is prioritized over battery conservation.

## Tailscale Exit-Node Roles

Exit-node setup has two separate responsibilities:

- Safehouse advertises the exit-node capability.
- A client chooses whether to use Safehouse as its exit node.

Keeping server-side and client-side steps separate makes the configuration easier to reason about and troubleshoot.

## Documentation Matters

Recording commands, failures, fixes, and why a change was made is as important as getting the configuration working. The goal of this repository is to preserve that process.
