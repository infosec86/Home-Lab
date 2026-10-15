# Lessons Learned

This page is less of a formal summary and more of a running list of things that actually clicked while I was building the lab.

## I keep having to ask: which machine am I on?

This sounds obvious, but it has probably been one of the most useful habits to build.

A lot of the networking work involves both a client and a server, and I have caught myself thinking about the right command on the wrong machine. Safehouse might be advertising an exit-node capability, but the client is the machine that chooses to use it. SSH configuration belongs on the server, but SSH keys and connection commands also have a client side.

Before I make a change now, I try to stop and ask whether I am on Safehouse, Nightfall, Windows, or inside a VM. That alone prevents a lot of confusion.

## Tailscale exit nodes made more sense once I separated the roles

At first I mixed up which machine was supposed to be the exit node.

Safehouse advertises that it can act as an exit node. My Acer, whether I am using Windows or Omarchy, is the client that decides whether to use Safehouse for internet traffic.

So a command such as:

```text
tailscale set --exit-node=<safehouse-address>
```

runs on the client. It means "send this computer's internet traffic through Safehouse." Once I thought of it that way, the setup stopped feeling backwards.

I also noticed the Tailscale `tx` and `rx` counters change much faster when the exit node is enabled. That gave me a visible sign that normal internet traffic was actually moving through the tunnel instead of only traffic headed to another tailnet device.

## `0.0.0.0` does not automatically mean "publicly exposed"

Glances gave me a warning that it was listening on:

```text
0.0.0.0:61208
```

My first thought was that I had exposed the dashboard more broadly than I wanted.

After checking `docker ps`, I saw that Docker was publishing the Glances port as:

```text
127.0.0.1:61208->61208/tcp
```

That helped me understand an important difference. Glances was listening on all interfaces inside the container, but Docker was only binding that container port to the loopback interface on the Safehouse host. Tailscale Serve was then forwarding the tailnet-only connection to that local port.

The lesson for me was not to judge exposure from one line of output. I need to look at the application, the container, the host binding, the firewall, and the remote-access layer together.

## A timeout and a rejected SSH key are completely different failures

I used to look at any failed SSH attempt as basically the same problem.

Now I separate them.

```text
Connection timed out
```

usually means I have not successfully reached the SSH service at all. That pushes me toward checking routing, Tailscale, firewall rules, interface state, or whether the service is running.

```text
Permission denied (publickey)
```

means I reached the server and the problem is authentication.

That distinction saves a lot of wasted troubleshooting.

When I need more detail, I use:

```bash
ssh -vvv <host>
```

The verbose output is noisy, but it shows which keys are being tried and where the connection is failing.

## My VMware network problem was a good example of troubleshooting by layers

After a brief power interruption, my Windows host still had internet access but the Xubuntu VMware guest did not.

Instead of assuming DNS was broken, I checked the guest interface and route, then tested an external IP address. Since raw IP connectivity also failed, I knew DNS was not the whole problem.

Because the host was online and only the guest was broken, I could narrow the problem to the virtual networking path instead of changing the home router or ISP settings.

The VM eventually reconnected and recovered, but the bigger lesson was to test one layer at a time instead of changing five things and hoping one works.

## Old commands still show up everywhere

I tried to use `ifconfig` on Safehouse and found that it was not installed. I also expected `ifconfig` to be the package name.

It is actually part of the older `net-tools` package, while modern Debian expects commands such as:

```bash
ip addr
```

or:

```bash
ip a
```

I installed `net-tools` because older tutorials and labs still use `ifconfig`, but I am trying to get more comfortable with the `ip` command because that is the modern toolset.

## tmux turned out to be more useful than I expected

I initially thought of tmux as mostly a terminal convenience, but it has become a nice way to watch several parts of Safehouse at once.

For example, I can keep a normal shell open, watch Docker in another pane, and keep Glances logs visible in another. It makes troubleshooting feel much more like working on a real server because I can watch the system while I change something instead of constantly opening and closing separate sessions.

## Cheap hardware is part of the lab, not a limitation I need to hide

Safehouse only has 4 GB of RAM. The Acer only has about 8 GB and the memory is soldered.

Instead of treating that as something embarrassing, I am starting to see it as part of the project. Resource limits force me to think about what a service actually needs, whether I should use a VM or a container, and when it really makes sense to buy more hardware.

The plan is still to add one inexpensive DDR4 corporate mini PC for Proxmox when I find a good deal, but I want each upgrade to solve a real problem instead of buying hardware just because homelabs are supposed to have it.

## Documentation works better when I record the confusion too

The original version of this page sounded too clean. It described concepts correctly, but it did not sound like the way I actually learned them.

The useful part of this lab is not just the final command. It is remembering that I misunderstood something, checking the system, finding the difference between what I assumed and what was actually happening, and then being able to explain it afterward.

That is the style I want to keep using in this repository.
