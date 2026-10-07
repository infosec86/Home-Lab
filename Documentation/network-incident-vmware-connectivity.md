# Network Incident Writeup: VMware Guest Connectivity Failure

## Summary

During normal home-lab use, a Linux guest running in VMware Workstation lost internet connectivity after a brief power interruption. The physical host retained normal internet access, while the guest experienced severe latency followed by complete loss of external connectivity.

This incident became a useful troubleshooting exercise because it occurred unexpectedly rather than as part of a planned lab.

## Environment

The affected environment consisted of:

- Windows host system
- VMware Workstation
- Linux desktop guest
- VMware NAT networking
- Standard non-administrative guest account for normal work
- Separate administrative guest account for system changes

Specific usernames, IP addresses, MAC addresses, VPN details, device identifiers, and other environment-specific values are intentionally omitted from this public writeup.

## Symptoms

The guest initially appeared extremely slow when accessing the internet. Further testing showed:

- The host system still had normal internet access.
- The guest could not reliably reach external IP addresses.
- Name resolution also failed.
- The guest network interface later reconnected and connectivity returned.

A failed connection to an external IP address was especially useful because it showed that the problem was more fundamental than DNS alone.

## Troubleshooting Process

The troubleshooting approach moved from the local virtual interface outward rather than changing multiple settings at once.

### 1. Verify interface state

```bash
ip addr
```

This checks whether the guest network interface is present, up, and has an IPv4 address.

### 2. Verify routing

```bash
ip route
```

The goal is to confirm that the guest has a valid default route through the virtual network.

A healthy system should include a default route similar to:

```text
default via <virtual-gateway> dev <guest-interface>
```

### 3. Test the virtual gateway

```bash
ping -c 4 <virtual-gateway>
```

This helps determine whether the problem exists between the guest and VMware's virtual network or farther upstream.

### 4. Test raw external connectivity

```bash
ping -c 4 <external-test-ip>
```

This test does not depend on DNS. If it fails, the problem is not simply name resolution.

### 5. Test DNS after IP connectivity

```bash
ping -c 4 example.com
```

If raw IP connectivity works but hostname resolution fails, DNS becomes the primary focus.

In this incident, both external IP connectivity and DNS were affected.

## Fault Isolation

The host system remained online while the guest could not reach the internet. That comparison significantly narrowed the fault domain.

Instead of investigating the ISP, household router, or browser first, the troubleshooting focus shifted to the guest's virtual network path:

```text
Guest interface
    ↓
Guest IP configuration
    ↓
Default route
    ↓
VMware virtual network / NAT
    ↓
External connectivity
    ↓
DNS
    ↓
Application
```

The guest eventually reported that its network interface had reconnected, after which connectivity returned.

## Likely Cause

The exact internal failure was not proven, so this writeup does not claim a definitive root cause.

Based on the observations, the most likely fault domain was the VMware virtual networking path or guest virtual NIC state following the abrupt power event.

Evidence supporting that conclusion:

- The physical host remained connected.
- The guest could not reach an external IP address.
- DNS failed at the same time as general connectivity.
- Connectivity returned when the guest's virtual network connection recovered.

## Resolution

Connectivity was restored after the guest's virtual network interface reconnected.

No router, ISP, or application-level changes were required.

## Lessons Learned

- Test external IP connectivity before assuming a DNS problem.
- Compare host and guest connectivity to isolate the fault domain.
- Check the guest interface and default route before changing application settings.
- Virtual NAT is an additional networking layer that can fail independently of the physical network.
- Unexpected infrastructure issues are valuable troubleshooting exercises when the symptoms, tests, reasoning, and outcome are documented.
- Avoid changing several variables at once; use each test to eliminate a specific layer of the stack.

## Interview Summary

A concise way to describe the incident in an interview:

> A Linux VM lost internet connectivity after a brief power interruption while the Windows host remained online. I separated DNS from general connectivity by testing an external IP address first. Because the guest could not reach the external IP, I knew the issue was below the DNS layer. I then checked the guest interface and routing path, narrowed the fault domain to the virtual networking layer, and verified recovery when the guest network interface reconnected. The incident reinforced a layered troubleshooting approach from interface to routing to external connectivity to DNS.

## Public Repository Safety

This writeup intentionally excludes:

- Real usernames
- Passwords or credentials
- VPN configuration details
- Public or private IP addresses from the actual environment
- MAC addresses
- Router or firewall administration details
- Device serial numbers
- Authentication tokens
- SSH keys or private key material
- Screenshots containing sensitive information

The goal is to document the troubleshooting method and technical reasoning without publishing information that could assist reconnaissance against the actual lab environment.
