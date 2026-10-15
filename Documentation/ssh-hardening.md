# SSH Hardening on Safehouse

SSH was one of the first things I wanted to get right on Safehouse because I planned to manage it remotely most of the time.

I did not want to expose a password-based SSH login to the internet and then just hope nobody found it. The approach I settled on was to keep SSH reachable through Tailscale and use public-key authentication.

## How I set it up

Safehouse uses OpenSSH with Ed25519 keys.

The client keeps the private key. Safehouse only gets the matching public key in the user's `authorized_keys` file. I also disabled password authentication and direct root SSH login.

That means I normally connect as a regular user and only use `sudo` when I actually need administrative privileges.

## What I had to understand

The part that took a little while to really stick was that SSH problems are not all the same.

If I see:

```text
Connection timed out
```

I probably have not reached the SSH service at all. That points me toward Tailscale, routing, firewall rules, interface state, or whether SSH is actually running.

If I see:

```text
Permission denied (publickey)
```

then the network path worked. I reached Safehouse, but authentication failed.

That distinction changed the way I troubleshoot SSH.

When I need more detail, I use:

```bash
ssh -vvv <user>@<host>
```

The output is noisy, but it shows which identities are being offered and whether the failure happens before or during authentication.

## Why I use Tailscale with SSH

I could forward port 22 through the home router, but there is no reason for me to do that right now.

Tailscale gives my authorized devices a private path to Safehouse, so SSH can stay off the public internet.

That does not mean I treat Tailscale as magic. I still want SSH itself configured correctly in case the network design changes later.

## How I verified it

I tested that I could connect with the key, confirmed password logins were disabled, confirmed direct root SSH was disabled, rebooted Safehouse, and verified that SSH still worked afterward.

I also added another authorized client and tested that separately so I could see how multiple client keys are handled.

## What I learned

SSH hardening made more sense once I stopped thinking of it as one setting.

There is the network path, the SSH service, the user account, file permissions, the public/private key relationship, and the authentication policy. A failure at any one of those layers can look like "SSH is broken" until I narrow down which part actually failed.
