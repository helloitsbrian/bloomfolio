---
title: "Self-Hosted Portfolio Website"
description: "A fully self-hosted personal portfolio website built with Astro and deployed on my home lab, served via NGINX in a Docker container and securely exposed to the internet using Cloudflare Tunnel."
image: "https://i.postimg.cc/qqnyrkcz/portfolio-website.png"
startDate: "2025-12-25"
skills: ["Astro", "Docker", "NGINX", "Linux", "Cloudflare Tunnel"]
---

## Self-Hosted Portfolio Website

This project documents the design, deployment, and hosting of my personal portfolio website, built with Astro and served entirely from my home lab infrastructure.

The site is statically generated and deployed using an NGINX container running inside an LXC environment. Rather than exposing inbound ports or relying on a public-facing server, external access is provided through a Cloudflare Tunnel, enabling secure, outbound-only connectivity from the lab to the internet.

The deployment emphasizes simplicity, security, and reproducibility. Content updates are managed through a Git-based workflow, with builds generated on the server and served as static assets. This project serves as a real-world example of combining modern static site tooling with containerization and zero-trust-style remote access.

**Key focus areas include:**
- Static site generation with Astro
- Containerized web serving with NGINX
- Secure internet exposure via Cloudflare Tunnel
- Linux-based self-hosted deployment and maintenance
