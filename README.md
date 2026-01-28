<div align="center">

# DYLARIS
### The Next-Generation Minecraft Infrastructure Ecosystem

[![Website](https://img.shields.io/badge/Website-bartisd.dev-blue?style=for-the-badge)](https://bartisd.dev)
[![Discord](https://img.shields.io/badge/Discord-Join%20Community-7289DA?style=for-the-badge)](DEIN_DISCORD_LINK)
[![Status](https://img.shields.io/badge/Status-Active%20Development-green?style=for-the-badge)]()

</div>

---

## 📖 About The Project

**Dylaris** is engineered to be a comprehensive web interface and infrastructure management system for game servers. While our roadmap includes full instance management, backups, and plugin orchestration, we have launched with the most critical foundation: **The Network Layer**.

Dylaris provides a high-performance, protocol-aware reverse tunneling system written in **Go**. It allows administrators to host services from restricted networks (Home/CGNAT) without port forwarding, while providing enterprise-grade DDoS protection through your own VPS gateways.

---

## ⚡ Module 1: The Network Layer (Dylaris Hub)

The current release focuses on intelligent ingress traffic management. Unlike generic TCP tunnels, Dylaris understands the application layer.

### Core Technologies
* **Protocol Parsers:** Custom Go implementations to inspect packet headers without terminating encryption prematurely.
    * **Minecraft:** Parses Handshake packet ID `0x00` to extract the target hostname.
    * **HTTPS:** Parses TLS Client Hello for SNI extraction.
    * **HTTP:** Parses Host Headers.
    * more services in the future
* **Multiplexing:** Utilizes `Hashicorp/Yamux` to handle concurrent streams over a single persistent connection.
* **Scalability:** Supports both a **Push Mode** (Direct Hub-to-Gate) and a **Redis Mode** (Cluster Discovery) for high availability.

### Architecture

The system is composed of three standalone binaries:

1.  **The Hub (Control Plane)**
    * Self-hosted web dashboard (Next.js/React + Go Fiber Backend).
    * Manages routes, licenses, and configuration distribution.
    * Includes an embedded Link agent for self-tunneling.
    * *Tech:* Go Fiber, GORM (SQLite/Redis), React.
    * **Hub includes an internal link**

2.  **The Gate (Ingress/Edge)**
    * Runs on a public VPS (the "Shield").
    * Accepts traffic on ports 80, 443, and 25565.
    * Routes traffic dynamically based on in-memory rules or Redis.
    * *Tech:* Go, Redis Client.

3.  **The Link (Agent)**
    * Runs on the backend server (Home/Lab).
    * Establishes the outbound connection to the Gate.
    * *Tech:* Yamux Session Management.

---

## 🗺️ Roadmap & Future Modules

Dylaris is evolving. The Networking Layer is just the start.

- [x] **Network Module** (Reverse Tunneling, SNI/Handshake Routing)
- [X] **Instance Manager** (Docker/Process management for MC Servers)
- [X] **File Manager** (Web-based file access)
- [ ] **User Management** (User & permission system)
- [ ] **Backup System** (Online/Local backups)
- [ ] **Plugin/Mod Manager** (One-click installs)
- [ ] **Modpack Support for Servers**

---

## 🚀 Getting Started

To deploy the Dylaris Network Layer:

1.  **Deploy the Hub** via Docker, read the Docs [Website](https://bartis.dev).
2.  **Deploy the Gate** on a public VPS with a static IP.
3.  **Run the Hub** on your local machine to access the dashboard.
4.  **Connect** your services using the Link Agent.

For detailed documentation, please visit **[Docs of Bartis.dev](https://bartisd.dev/docs)**.

---

## 🐛 Issue Tracking

This repository serves as the central issue tracker for the Dylaris ecosystem.
If you encounter bugs with the Hub, Gate, or Link, please open an issue here.

---

<div align="center">
  <sub>Built with ❤️ in Go, NextJS & TailwindCSS by Bartis.</sub>
</div>
