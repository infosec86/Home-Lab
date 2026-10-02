# SSH Hardening

## Objective

The goal of this configuration is to administer Safehouse remotely while reducing unnecessary SSH exposure and avoiding password-based remote authentication.

## Authentication

Safehouse uses OpenSSH with Ed25519 public-key authentication.

The private key remains on the client device and is protected with a passphrase. The corresponding public key is stored in the server user's `authorized_keys` file.

Password-based SSH authentication is disabled, and direct root SSH login is disabled. Administrative tasks are performed from a normal user account with `sudo` only when elevated privileges are required.

## Network Access

SSH is primarily reached through Tailscale instead of exposing port 22 directly to the public internet.

## Troubleshooting

A useful troubleshooting sequence is:

```bash
tailscale status
tailscale ping <SERVER_NAME>
ssh -vvv <USER>@<SERVER_TAILSCALE_IP>
```

The verbose SSH output helped distinguish between:

- Network timeouts
- Hostname-resolution problems
- Missing client identities
- Rejected public keys
- Successful network connectivity with failed authentication

One important lesson was to always verify which machine a command is running on before changing server or client configuration.

## Verification

The setup has been tested by:

- Connecting with an SSH key
- Confirming password authentication is disabled
- Confirming root SSH login is disabled
- Rebooting the server
- Verifying SSH connectivity after reboot
- Adding a second authorized client key and testing it successfully

## What I Learned

This work reinforced the relationship between SSH authentication, Linux permissions, public/private key pairs, remote administration, network connectivity, and reducing unnecessary exposure.
