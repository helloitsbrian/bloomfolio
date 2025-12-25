---
title: "Secure Remote Access with Cloudflare Zero Trust"
description: "A secure remote access architecture built with Cloudflare Tunnels and Zero Trust Access to expose self-hosted services without opening firewall ports, using identity-aware authentication and per-application access controls."
image: "https://i.postimg.cc/hv3xcspN/cloudflare-zero-trust.png"
startDate: "2025-11-30"
skills: ["Cloudflare Zero Trust", "Cloudflare Tunnels", "Networking", "Security"]
---

## Overview

I designed and implemented a secure remote access model for my self-hosted services using Cloudflare Tunnels and Zero Trust Access. The goal was to make internal services available from anywhere **without exposing ports, managing dynamic IPs, or relying on VPNs**, while still enforcing strong authentication boundaries.

This setup now protects all externally accessible services in my homelab.

## Problem

Running multiple self-hosted services (Proxmox UI, media services, photo management, dashboards) required remote access, but traditional approaches introduced risk:

- Port forwarding exposed services directly to the internet
- Dynamic residential IPs complicated DNS and firewall rules
- VPNs added friction and single points of failure
- Per-service authentication was inconsistent or nonexistent

I wanted a solution that prioritized **security, simplicity, and maintainability**.

## Constraints

- Home network with no static public IP
- No inbound ports allowed through the firewall
- Multiple internal services on different hosts and ports
- Access limited to specific users and identity providers
- Minimal operational overhead

## Solution

I implemented a Zero Trust access layer using Cloudflare Tunnels and Cloudflare Access:

- Deployed Cloudflare Tunnel (`cloudflared`) from inside the network to create outbound-only connections
- Routed individual subdomains to internal services through tunnel ingress rules
- Enforced authentication per service using Cloudflare Access
- Integrated Google SSO to restrict access to approved identities
- Applied per-application policies instead of network-wide trust

**No services are directly exposed to the internet, and no ports are opened on the firewall.**

## Architecture
```
+------------------+
|  User Browser    |
+--------+---------+
         |
         | HTTPS
         v
+------------------------------+
|  Cloudflare Edge             |
|  - Zero Trust Access         |
|  - Identity Authentication   |
+--------+---------------------+
         |
         | Encrypted Tunnel
         | (outbound-only)
         v
+------------------------------+
|  Cloudflare Tunnel           |
|  (cloudflared)               |
+--------+---------------------+
         |
         v
+--------------------------------------------+
|  Internal Services (Private Network)       |
|  - Proxmox                                 |
|  - Immich                                  |
|  - Dashboards / Applications               |
|  - No public IP exposure                   |
+--------------------------------------------+
```
Each service is accessed via its own subdomain and protected independently.

## Stack

- Cloudflare Tunnel (`cloudflared`)
- Cloudflare Access (Zero Trust)
- DNS-based routing
- Google SSO
- Docker / systemd for tunnel management
- Proxmox-hosted services behind private IPs

## Outcome

- Secure, authenticated access to all services from any location
- Zero exposed ports on the home firewall
- No dependency on VPN clients or device-level configuration
- Per-service access control instead of implicit network trust
- Simple onboarding and offboarding by identity

This approach significantly reduced attack surface while improving usability.

## What I Learned

- Zero Trust models scale better than network-based trust, even in small environments
- Identity-aware access simplifies security management
- Outbound-only tunnels eliminate entire classes of firewall and NAT issues
- Per-application policies are easier to reason about than global access rules

## Future Improvements

- Add device posture checks for additional access control
- Implement service-specific MFA requirements
- Add monitoring and alerting for tunnel health
- Document standardized ingress patterns for faster service onboarding