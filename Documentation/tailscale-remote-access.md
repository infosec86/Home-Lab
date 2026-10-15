# Tailscale Remote Access and Exit Node

Tailscale started as a way for me to reach Safehouse without opening ports on my home router. It has turned into one of the more useful parts of the lab because it also gave me a practical way to learn about private networking, routing, and exit nodes.

## Remote access

Safehouse and my client systems are on the same tailnet. That lets me SSH into Safehouse from Windows or Omarchy even when I am not on the same local network.

The basic path is: Acer / remote client -> encrypted Tailscale tunnel -> Safehouse -> SSH, Glances, and other private services.

I like this because I do not have to expose SSH or Glances directly to the public internet just to reach them remotely.

## The exit-node part that confused me at first

I originally mixed up which machine was supposed to do what.

Safehouse is the machine that advertises the exit-node capability. My Acer is the client that decides whether to use Safehouse as the route to the internet.

So the client-side command points to Safehouse:

```text
tailscale set --exit-node=<SAFEHOUSE_TAILSCALE_IP>
```

That means, in plain language, "send this computer's internet traffic through Safehouse."

Once I started thinking of it that way, the setup became much easier to understand.

## Windows shortcuts

On Windows I created two PowerShell functions:

```powershell
safehouse-on
safehouse-off
```

Those functions live in my PowerShell profile and save me from remembering the full Tailscale command every time.

I also had to change my PowerShell execution policy for the current user to `RemoteSigned` so the profile could load. I did not use `Unrestricted` or disable script security system-wide.

## Omarchy shortcuts

I set up the same idea in Omarchy so the workflow is consistent no matter which OS I boot on the Acer:

```bash
safehouse-on
safehouse-off
```

The implementation is different because Linux uses shell aliases/functions while Windows uses PowerShell functions, but the result is the same.

## How I verified it was actually working

One of the easiest signs was `tailscale status`.

When Safehouse was only available as an option, the status showed that it `offers exit node`. After enabling it from the client, the status changed to show Safehouse as the active exit node.

I also noticed the `tx` and `rx` counters increase much faster with the exit node enabled. That made sense once I realized normal internet traffic was now crossing the Tailscale tunnel instead of only traffic going to other tailnet devices.

## What this gives me when traveling

If I am on hotel or public Wi-Fi, I can still connect directly to Safehouse for SSH and lab services without using it as an exit node.

Or I can enable the exit node and route my internet traffic back through my home connection: Acer while traveling -> encrypted Tailscale tunnel -> Safehouse at home -> home internet -> internet.

This is not the same thing as using a commercial privacy VPN. Websites still see the public IP of my home internet connection. The value for me is secure remote access and the ability to use my own home network as the exit point when I am away.

## What I learned

The biggest lesson here was separating private-network access from internet routing. Tailscale can connect my devices together without automatically routing all web traffic through Safehouse. The exit-node setting is what changes that behavior.

That distinction is something I understand much better now because I could actually turn it on, watch the route change, and see the traffic counters move.
