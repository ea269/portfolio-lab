---
title: "Hardened Portfolio Infrastructure"
date: 2026-02-22
description: "Deploying a professional, zero-trust Hugo portfolio on Proxmox."
summary: "An engineering-focused dive into hypervisor-based hosting, Cloudflare Tunnel integration, and CI/CD sanitization."
tags: ["Proxmox", "Cloudflare", "Hugo", "Linux Administration", "Security"]
categories: ["Infrastructure"]
showAuthor: false
showTableOfContents: true
---

![Website Home Page](/images/website.png)

## 🎯 Project Vision
The goal was to move beyond traditional hosting and engineer a **production-grade web environment** that prioritizes security, persistence, and privacy. This project serves as a live demonstration of my ability to manage the full technical stack—from the hypervisor to the public domain.

## 🏗️ Architecture & Technical Stack
* **Hypervisor:** **Proxmox VE (LXC)** — Utilized for lightweight, isolated containerization.
![Proxmox Dashboard](/images/proxmox-dash.png)
* **Networking:** **Cloudflare Tunnel (Argo)** — Provides "Zero-Trust" ingress, exposing the site without opening firewall ports or leaking my home IP.
* **Web Engine:** **Hugo (Extended)** — A high-performance static site generator utilizing the Blowfish theme.
* **OS:** **Debian 12** — Hardened Linux environment managed via SSH.

![Network Architecture Diagram](/images/architecture-diagram.jpeg)

## 🛠️ Key Implementation & Problem Solving
### 1. High Availability via Systemd
I transitioned the environment from interactive testing to a persistent production state by creating custom **systemd unit files**. This ensures that both the web server and the network tunnel auto-start on boot and recover instantly from failures.
![Systemd Service Status](/images/service-status.png)
![Systemd Cloudflare Status](/images/cloudflare-status.png)

### 2. Operational Security (OPSEC) & Sanitization
A critical phase involved a "History Sanitization" audit. I purged internal network identifiers (IPv4 192.168.x.x) from the Git history and the Hugo build artifacts to ensure zero information leakage to the public.

## 🔒 Security Hardening
* **No Inbound Ports:** The environment has **zero** open ingress ports; the Cloudflare daemon creates an outbound-only connection to the edge network.
![Cloudflare Tunnel Dashboard](/images/cloudflare-dash.jpeg)
* **Artifact Integrity:** Implemented a strict `.gitignore` policy to prevent the leakage of sensitive build metadata and local file paths.
* **Persistence:** Configured `Restart=always` policies for all services to mitigate downtime.

## 📈 Professional Takeaways
* **Security-First Mindset:** Demonstrated through the proactive sanitization of the version control history.
* **Infrastructure Ownership:** Managed the end-to-end lifecycle from provisioning hardware to configuring public DNS.
* **Resilience:** Successfully troubleshot and resolved "502 Bad Gateway" and network binding issues using system-level tools.
