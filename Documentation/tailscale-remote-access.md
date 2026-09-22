\# Tailscale Remote Access



\## Objective



I wanted secure remote access to my Safehouse home lab without exposing administrative services directly to the open Internet.



\## Configuration



Tailscale was installed on the Safehouse server and my client computer.



The server is accessed over the private Tailscale network rather than through port forwarding on my home router.



SSH is used over the Tailscale connection for remote administration.



\## Security Approach



Using Tailscale allows me to avoid directly exposing SSH to the open Internet.



Access is limited to authenticated devices that are members of my private tailnet.



\## Testing



I have verified that:



&#x20;Safehouse could be reached remotely over Tailscale

&#x20;SSH connections worked after reboot

&#x20;The server remained accessible with the laptop lid closed

&#x20;Internal services could be accessed without public port forwarding



\## What I Learned So Far



This project helped me understand private overlay networks, secure remote administration, encrypted connectivity, and reducing unnecessary Internet exposure.

