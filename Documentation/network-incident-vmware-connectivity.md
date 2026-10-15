# VMware Guest Lost Network Connectivity

This was not a lab I planned. It happened after a brief power interruption, which made it more useful because I had to troubleshoot a real problem instead of following a checklist.

My Windows host still had internet access, but the Xubuntu VM in VMware Workstation became extremely slow and then lost outside connectivity completely.

## What I noticed first

The important detail was that Windows was still online while the VM was not. That meant I probably did not need to start changing the home router, blaming the ISP, or resetting everything in sight.

The problem looked much more likely to be somewhere between the guest operating system and VMware's virtual network.

## What I checked

I started inside the Xubuntu guest with:

```bash
ip addr
```

I wanted to know whether the virtual interface was still present, whether it was up, and whether it had an IPv4 address.

Then I checked the route table:

```bash
ip route
```

I was looking for a valid default route through VMware's virtual gateway.

From there I tested outward instead of jumping straight to DNS.

First the virtual gateway:

```bash
ping -c 4 <virtual-gateway>
```

Then an external IP address:

```bash
ping -c 4 <external-test-ip>
```

Then a hostname:

```bash
ping -c 4 example.com
```

The external IP test mattered because it does not depend on DNS. Since that failed too, I knew the problem was below the name-resolution layer.

## What that told me

The host had internet access, but the guest could not reach an external IP. That narrowed the fault domain quite a bit.

I started thinking about the path as: Xubuntu guest -> virtual NIC -> VMware NAT / virtual network -> Windows host -> home network / internet.

I did not prove an exact internal VMware root cause, so I do not want to pretend I did. The best conclusion I could support was that the problem was somewhere in the guest virtual NIC or VMware NAT path after the power interruption.

Eventually the guest reported that the interface had reconnected, and internet access returned without changing the router or ISP configuration.

## What I learned from it

The biggest lesson was not "restart VMware." It was learning how much faster troubleshooting gets when I compare a working system to a broken one and test one layer at a time.

If I had gone straight to DNS settings, I would have been troubleshooting the wrong layer. If I had reset the router first, I would have changed something that was already working.

The sequence that made sense was: interface -> route -> virtual gateway -> external IP -> DNS -> application.

That is the part I want to remember for future problems.

## How I would explain this in an interview

A Linux VM lost internet access after a brief power event while the Windows host remained online. I used the working host as a comparison point, checked the guest interface and routing, and tested an external IP before looking at DNS. Because raw IP connectivity failed, I knew the problem was below the DNS layer. That narrowed the issue to the VMware virtual networking path, and connectivity returned when the guest interface recovered.

## What I left out of the public repo

I intentionally removed real usernames, device addresses, VPN details, MAC addresses, credentials, and other information that would not add anything to the troubleshooting story.
