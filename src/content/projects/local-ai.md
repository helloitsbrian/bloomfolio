---
title: "Local LLM with Open‑WebUI"
description: "I enjoy using ChatGPT, but the idea of sending every prompt to a distant data center made me uneasy. I wanted a way to keep my brainstorming private, avoid the hidden energy cost of cloud APIs, and still enjoy the same level of assistance."
image: "https://i.postimg.cc/KvNSRxn2/local-ai.png"
startDate: "2025-11-30"
skills: ["Ollama", "Open-WebUI", "Proxmox Virtual Environment", "Docker", "Cloudflare", "Zero Trust"]
---

## Project Overview

This project documents my journey building a fully self-hosted local large language model (LLM) environment that delivers a ChatGPT-like experience without relying on cloud APIs.

The goal of this project was to create a private, fast, and flexible AI environment that I control end-to-end, while maintaining a polished, browser-based user experience.

## Architecture Overview

At a high level, the system consists of:

- A **Proxmox Virtual Environment** acting as the hypervisor
- A dedicated Linux VM running Docker
- **Ollama** for local model serving
- **Open-WebUI** as the primary user interface
- **Cloudflare Tunnel + Zero Trust** for secure remote access

All inference runs locally on my own hardware. No prompts or responses are sent to third-party APIs.

## Core Technologies

- **Hypervisor**: Proxmox Virtual Environment
- **Container Runtime**: Docker
- **Model Runtime**: Ollama
- **Web Interface**: Open-WebUI
- **Access Layer**: Cloudflare Tunnel
- **Security**: Cloudflare Zero Trust (SSO-gated)
- **Models**: Mix of open-weight models (Mistral, Gemma, Qwen, GPT-OSS, etc.)

## Local Model Serving (Ollama)

Ollama handles all model management and inference locally. It provides:

- Simple model installation and versioning
- Quantized model support for efficient GPU utilization
- A clean local API that Open-WebUI can consume
- The ability to swap models on demand without re-architecting the system

This setup allows me to experiment with multiple models, compare performance and response quality, and tune inference behavior based on hardware constraints.

## User Interface (Open-WebUI)

Open-WebUI provides a polished, ChatGPT-like experience while remaining fully self-hosted.

Key features I rely on:
- Browser-based chat interface
- Conversation history and session persistence
- Model switching per conversation
- System prompts and personality tuning
- Multi-user support (behind Zero Trust)

The UI runs entirely inside Docker and communicates only with the local Ollama instance.

## Security & Remote Access

Rather than exposing ports directly to the internet, I use **Cloudflare Tunnel** to publish the service securely.

Access is protected by **Cloudflare Zero Trust**, which allows me to:
- Restrict access to specific identities
- Enforce SSO authentication
- Eliminate the need for port forwarding
- Keep the service private while still accessible remotely

This approach mirrors how I would expose internal tools in a production environment.

## Performance & Tradeoffs

Running models locally introduces real constraints — GPU memory, VRAM bandwidth, and power consumption all matter. I’ve learned to balance:

- Model size vs. response quality
- Quantization level vs. speed
- GPU utilization vs. system responsiveness

While local models don’t always match the absolute quality of frontier cloud models, the tradeoff is worth it for privacy, cost control, and transparency.

## What I Learned

This project significantly deepened my understanding of:

- LLM inference pipelines
- GPU-accelerated workloads in virtualized environments
- Docker-based service composition
- Secure service exposure without traditional VPNs
- The practical limitations of consumer-grade AI infrastructure

More importantly, it reinforced that modern AI systems are *infrastructure problems* as much as they are model problems.

