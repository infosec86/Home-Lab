# SSH Hardening

## Objective

The purpose of this configuration was to securely administer the Safehouse server remotely while reducing the risk associated with password based SSH authentication.

## Initial Configuration

Safehouse uses OpenSSH for remote administration.

The server is accessed remotely using my primary Linux account, not the root account.

## SSH Key Authentication

I configured Ed25519 public-key authentication for remote access.

Ed25519 was selected because it provides modern cryptographic security while using relatively small keys.

The private SSH key remains on the client device and is protected with a passphrase.

The corresponding public key is installed on the Safehouse server.

## Password Authentication

After confirming that SSH key authentication was working correctly, password-based SSH authentication was disabled.

This reduces the server's exposure to password guessing and brute-force authentication attacks.

## Root SSH Access

Direct SSH access to the root account was disabled.

Administrative tasks are instead performed through my normal user account using `sudo` when elevated privileges are required.

## Remote Access

SSH access is primarily performed over tailscale rather than exposing the SSH service directly to the public Internet.

## Verification

The configuration was tested by:

• Connecting to Safehouse using an SSH key
• Confirming password-based SSH authentication was disabled
• Confirming root SSH login was disabled
• Rebooting the server
• Verifying SSH connectivity after reboot

## What I Learned so far

This project has helped me understand the relationship between SSH authentication, Linux user permissions, public/private key pairs, remote administration, and reducing unnecessary network exposure.
