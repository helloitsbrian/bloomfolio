---
title: "Home Server Build"
description: "A custom-built home server used as a self-hosted platform for infrastructure, automation, and local application workloads, designed to support experimentation, learning, and long-running services."
image: "https://i.postimg.cc/9MmVx0tW/home-server-build.png"
startDate: "2025-11-25"
skills: ["Proxmox Virtual Environment", "Docker", "Linux", "Networking"]
---

## Overview

This project documents the design and ongoing operation of my personal home server, which I use as a self-hosted platform for running and managing a variety of services.

Instead of building a single-purpose machine, I approached the server as modular infrastructure: workloads are isolated, resources are allocated deliberately, and services can be added, updated, or removed without impacting the rest of the system.

The server acts as the underlying foundation for several other projects in my portfolio, including media services, automation tools, document management, and locally hosted applications.

## System Design

The server runs **Proxmox Virtual Environment** as its hypervisor, allowing me to separate workloads across virtual machines and containers based on their requirements.

Applications are primarily deployed using **Docker**, making services easier to manage, update, and troubleshoot over time. Persistent data is stored on networked storage and mounted only where needed.

## Hardware Specs

- **Motherboard:** MSI B550M-Pro VC WiFi  
- **CPU:** AMD Ryzen 7 5700X  
- **Memory:** 64GB DDR4 @ 3200 MT/s  
- **GPU:** GIGABYTE GeForce RTX 5060 Ti  

## Why This Project Matters

Operating this server has given me hands-on experience managing infrastructure as a living system, balancing performance, reliability, and maintainability over time.

It serves as both a practical learning environment and the backbone for the other self-hosted projects I actively use and maintain.