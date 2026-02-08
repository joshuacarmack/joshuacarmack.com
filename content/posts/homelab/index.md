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

At a high level, everything at home centers around a Proxmox cluster. Most workloads run either as VMs or Docker containers inside VMs. A Synology NAS handles bulk storage and is also part of the backup chain. Some public-facing services live on a small set of Linode VPS instances.

I try to keep a clear separation between:

- Network edge (firewall / routing)
- Virtualization layer
- Container layer
- Storage
- External VPS

Most inbound access is handled through Cloudflare Tunnel instead of traditional port forwarding.

---

## Network Design

### Hardware

- UniFi UDM-Pro (gateway / firewall)
- UniFi Core Switch
- UniFi Office Switch
- UniFi Access Points

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
- Cloudflare Tunnel used for most public access  
- Very minimal direct port forwarding  
- Internal services are not exposed unless necessary  

---

## Virtualization Layer (Proxmox)

All local compute runs in a single Proxmox cluster named `Home`.

### Cluster Nodes

| Node | IP | CPU | RAM | Notes |
|-----|----|----|----|------|
| jc-pve01 | 192.168.4.21 | Dual Xeon E5620 | ~82 GB | Older but reliable |
| jc-pve02 | 192.168.4.22 | i5-4570T | 4 GB | Lightweight node |
| jc-pve03 | 192.168.4.23 | i5-4570T | ~8 GB | Lightweight node |
| jc-pve04 | 192.168.4.24 | Xeon Silver 4110 | ~96 GB | Primary heavy host |

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

Stacks are grouped by function:

- monitoring  
- media  
- automation  
- infrastructure  
- utility  

This keeps things organized and easier to back up or migrate.

---

## Core Services

### Monitoring

- Grafana  
- Prometheus  
- Zabbix Proxy  
- Uptime Kuma  
- InfluxDB  

### Media

- Jellyfin  
- Radarr  
- Sonarr  
- SABnzbd  
- Immich  
- MeTube  

### Automation

- Node-RED  
- n8n  

### Infrastructure

- Caddy  
- Cloudflared  
- MQTT Broker  
- Gitea  
- Gitea Mirror  
- ArchiveBox  

### Utility

- Paperless-NGX  
- Hoarder  
- HomeBox  
- Pairdrop  
- RustDesk  
- ITFlow  

---

## External Infrastructure (Linode)

I use a few small VPS instances mainly for:

- Public Docker workloads  
- RustDesk relay  
- TacticalRMM  
- Offsite monitoring and backups  

This keeps public exposure away from my home network when possible.

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
- Containers grouped by stack  
- Avoid snowflake configs where possible  
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