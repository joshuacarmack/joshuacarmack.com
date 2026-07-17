---
title: "My Homelab"
date: 2026-02-08
draft: true
summary: "An overview of my homelab and applications I run."
tags: ["server","automation","homelab","programming","proxmox"]
---

# My Homelab – Architecture, Design, and Why I Built It

This post is the first in a small series documenting my homelab. I use this environment for a mix of self-hosting, media services, automation, monitoring, and general experimentation. It also supports a handful of side projects, club infrastructure, and tools I rely on regularly.

The goal has never been “enterprise perfect.” The goal is:

- Reliable enough to trust  
- Flexible enough to experiment  
- Simple enough to recover when something breaks  

This document is meant to be a living reference for me and a starting point for anyone curious about how it’s put together.

---

## High-Level Architecture

At a high level, everything at home centers around a Proxmox cluster. Most workloads run either as VMs, Containers, or Docker containers inside VMs. A Synology NAS handles bulk storage and is also part of the backup chain. Some public-facing services live on a small set of Linode VPS instances.

I try to keep a clear separation between:

- Network edge (firewall / routing)
- Virtualization layer
- Container layer
- Storage
- External VPS

Most inbound access is handled through Caddy as a reverse proxy or Cloudflare Tunnels.

---

## Network Design

### Hardware

- UniFi UDM-Pro (gateway / firewall)
- UniFi Core Switch
- UniFi Office Switch
- UniFi Access Point

Everything network-wise is UniFi, which keeps management simple.

### VLANs

| VLAN | Name | Purpose |
|-----:|-----|--------|
| 1 | default | Internal LAN |
| 9 | public-servers | Public-facing services |
| 99 | sandbox | Testing / experiments |

Most infrastructure lives on the default VLAN. Public services are placed on VLAN 9. Anything risky or experimental goes into VLAN 99.

### Security Approach

- UDM-Pro handles firewalling  
- Cloudflare Tunnel or Caddy reverse proxy used for most public access  
- Very minimal direct port forwarding  
- Internal services are not exposed unless necessary  

---

## Virtualization Layer (Proxmox)

All local compute runs in a single Proxmox cluster named `Home`.

### Cluster Nodes

| Node | CPU | RAM | Notes |
|-----|----|----|----|------|
| jc-pve01 | Dual Xeon E5620 | ~82 GB | Older but reliable |
| jc-pve02 | i5-4570T | 4 GB | Lightweight node |
| jc-pve03 | i5-4570T | ~8 GB | Lightweight node |
| jc-pve04 | Xeon Silver 4110 | ~96 GB | Primary heavy host |

Not all nodes are equal, and that’s okay. Heavier workloads tend to land on jc-pve04.

### Storage Layout

- Local-lvm on each node  
- Proxmox Backup Server (PBS)  
- Synology NAS  

---

## Container Platform

Docker runs inside VMs rather than directly on Proxmox hosts.

- One Docker VM at home  
- One Docker VM on Linode  

I manage containers using Dockge and Docker Compose.

---

## Core Services

### Monitoring

- **Grafana** – Dashboards and visualization for metrics collected across the homelab.
- **Prometheus** – Metrics collection and time-series storage that feeds the Grafana dashboards.
- **Zabbix** – Infrastructure monitoring and alerting across hosts and services.
- **Uptime Kuma** – Lightweight uptime/status checks with notifications and public views.
- **InfluxDB** – Time-series database, mostly used for sensor and IoT data.
- **Rybbit** – Privacy-friendly web analytics for my sites.

### Media

- **Jellyfin** – Self-hosted media server for movies and TV.
- **Radarr** – Automates movie downloads and library management.
- **Sonarr** – Automates TV show downloads and library management.
- **SABnzbd** – Usenet download client feeding Radarr and Sonarr.
- **Immich** – Self-hosted photo and video backup, like a private Google Photos.
- **BirdNET** – Identifies bird species from audio picked up around the property.
- **ADS-B Tracker** – Tracks aircraft overhead using an SDR receiver. Public feed: [adsb.joshuacarmack.com](https://adsb.joshuacarmack.com).
- **Restreamer** – Restreams IP camera and RTMP feeds for local viewing and recording.

### Automation

- **Node-RED** – Flow-based automation for IoT and integration tasks.
- **n8n** – Workflow automation for connecting apps and APIs.
- **Cronicle** – Scheduled job runner for scripts and recurring tasks.

### Infrastructure

- **Caddy** – Reverse proxy in front of most self-hosted services, with automatic HTTPS.
- **Cloudflared** – Cloudflare Tunnel client for exposing services without opening ports.
- **EMQX (MQTT Broker)** – Message broker for IoT devices and automation.
- **Gitea** – Self-hosted Git server for personal and club repos.
- **Gitea Mirror** – Keeps Gitea repos synced with GitHub.
- **Home Assistant** – Central hub for smart home automation: lights, sensors, and other connected devices.
- **FreePBX** – Self-hosted VoIP/phone system.

### Utility

- **Paperless-NGX** – Document scanning and archiving with OCR search.
- **Hoarder** – Bookmark and link archiving tool.
- **HomeBox** – Tracks household/homelab inventory: hardware, spare parts, and other physical assets.
- **HomeBox Companion** – Companion app for scanning items into HomeBox.
- **ITFlow** – MSP-style documentation and client management, used for a side project.
- **BentoPDF** – Web-based PDF toolkit for merging, splitting, and converting files.
- **CommaFeed** – Self-hosted RSS reader.
- **Invoice Ninja** – Invoicing and billing for side projects.
- **IT-Tools** – Collection of handy utilities for developers and sysadmins.
- **Networking Toolbox** – Networking utilities like subnet calculators and DNS lookups.
- **Mixpost** – Social media scheduling and posting.
- **OnTime** – Event and stage timer for livestreams and presentations.

---

## Highlights

A few of these get a callout since I rely on them the most day-to-day: **Zabbix**, **Caddy**, **HomeBox**, and **Home Assistant** (see descriptions above). My **ADS-B Tracker** is also public if you want to see what's flying overhead: [adsb.joshuacarmack.com](https://adsb.joshuacarmack.com).

---

## External Infrastructure (Linode)

I use a few small VPS instances mainly for:

- Public Docker workloads  
- TacticalRMM  
- Offsite monitoring

This keeps important applications offsite with redundancy.

---

## Backups & Disaster Recovery

Backup flow:

VMs / Containers
↓
Proxmox Backup Server
↓
Synology NAS
↓
Backblaze B2

This gives me:

- Fast local restores  
- Protection from single-disk failure  
- Offsite copy for worst-case scenarios  

Nothing fancy, just layered.

---

## Operational Practices

- Clear naming (jc-pveXX, descriptive VM names)  
- If something is annoying to rebuild, it gets backed up  

---

## Lessons Learned (So Far)

- Clusters don’t have to be identical to be useful  
- Backups matter more than perfect architecture  
- Containers inside VMs are a good compromise for flexibility  
- Documentation saves future-me a lot of time  

---

## Roadmap

- Better documentation  
- Add NetBox or similar for inventory  
- More automation around backups and monitoring  
- Possibly add another small node in the future  

---

## Closing

This is a living setup and a living document. I’ll update this as things evolve and plan to do deeper-dive posts on Proxmox, Docker, and monitoring later.