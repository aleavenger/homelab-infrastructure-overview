# Homelab Infrastructure

**Self-hosted infrastructure environment for system prototyping and production workloads.**

> Two-node Proxmox cluster managing 100+ containers — DNS, firewalls, networking, backups, and isolated development environments for SaaS systems, APIs, and automation pipelines.

---

## Overview

A production-grade self-hosted infrastructure environment used to prototype, test, and deploy SaaS systems, automation pipelines, and development tools. This homelab serves as the backbone for all project development and hosting — from CI/CD runners to database clusters to AI agent execution environments.

### Key Capabilities

- **Proxmox Cluster** — Two-node HA cluster with live migration and resource pooling
- **100+ Containers** — LXC and Docker containers across isolated VLANs
- **Network Architecture** — DNS, reverse proxy, firewall rules, VLAN segmentation
- **Backup & Recovery** — Automated backup strategies with off-site replication
- **Development Environments** — Isolated workspaces for SaaS development and testing
- **Service Hosting** — Production workloads including databases, APIs, monitoring

---

## Architecture

```
                        ┌──────────────────┐
                        │    Internet      │
                        └────────┬─────────┘
                                 │
                        ┌────────▼─────────┐
                        │    Firewall      │
                        │  (rules + NAT)   │
                        └────────┬─────────┘
                                 │
                    ┌────────────┼────────────┐
                    │                         │
           ┌────────▼─────────┐    ┌──────────▼────────┐
           │   Proxmox Node 1 │    │  Proxmox Node 2   │
           │                  │◄──►│                    │
           │  ┌────────────┐  │    │  ┌────────────┐   │
           │  │ LXC / VMs  │  │    │  │ LXC / VMs  │   │
           │  │ (50+ each) │  │    │  │ (50+ each) │   │
           │  └────────────┘  │    │  └────────────┘   │
           └──────────────────┘    └───────────────────┘
                    │                         │
                    └────────────┬────────────┘
                                 │
              ┌──────────┬───────┼───────┬──────────┐
              │          │       │       │          │
         ┌────▼───┐ ┌───▼──┐ ┌──▼──┐ ┌──▼───┐ ┌───▼────┐
         │  DNS   │ │ DBs  │ │ Dev │ │ Media│ │ Monitor│
         │ + Proxy│ │ PG,  │ │ Env │ │ Srv  │ │ + Logs │
         └────────┘ │ Redis│ └─────┘ └──────┘ └────────┘
                    └──────┘
```

---

## Infrastructure Components

### Virtualization
| Component | Details |
|-----------|---------|
| **Hypervisor** | Proxmox VE (2 nodes, clustered) |
| **Containers** | 100+ LXC containers + Docker stacks |
| **VMs** | Specialized workloads (Windows, isolated testing) |
| **Storage** | Local ZFS + shared NFS for live migration |

### Networking
| Component | Details |
|-----------|---------|
| **DNS** | Self-hosted DNS with internal zone management |
| **Reverse Proxy** | Nginx Proxy Manager / Traefik for service routing |
| **Firewall** | Rule-based with VLAN segmentation |
| **VLANs** | Isolated networks: production, dev, management, DMZ |
| **VPN** | Secure remote access to internal services |

### Storage & Backups
| Component | Details |
|-----------|---------|
| **Primary Storage** | ZFS pools with compression and snapshots |
| **Backup Strategy** | Automated daily backups with retention policies |
| **Off-Site** | Replicated backups to secondary location |
| **Recovery** | Tested restore procedures for critical services |

### Monitoring & Observability
| Component | Details |
|-----------|---------|
| **Metrics** | Prometheus + Grafana dashboards |
| **Logging** | Centralized log aggregation |
| **Alerting** | Threshold-based alerts for resource usage |
| **Health Checks** | Automated service monitoring |

---

## Hosted Services

### Development Infrastructure
- Git repositories and CI/CD runners
- Docker registries
- Development databases (PostgreSQL, Redis)
- Isolated SaaS testing environments

### Production Workloads
- API servers (FastAPI, Express.js)
- Database clusters (PostgreSQL)
- Message queues and job runners
- AI agent execution environments (PaperclipAI)

### System Services
- DNS and DHCP
- Reverse proxy and TLS termination
- VPN gateway
- Monitoring and alerting stack
- Backup orchestration

### Media & Personal
- Media server and management
- File sharing and sync
- Home automation integration

---

## Tech Stack

| Category | Technologies |
|----------|-------------|
| **Hypervisor** | Proxmox VE |
| **Containers** | Docker, LXC |
| **Operating Systems** | Debian, Ubuntu Server, Alpine |
| **Networking** | VLANs, DNS, Nginx, Traefik, WireGuard |
| **Storage** | ZFS, NFS, Samba |
| **Monitoring** | Prometheus, Grafana, Uptime Kuma |
| **Automation** | Ansible, shell scripts, cron |
| **Databases** | PostgreSQL, Redis, SQLite |
| **Backup** | Proxmox Backup Server, rsync |

---

## What This Enables

This infrastructure serves as the foundation for all other projects:

- **Invoice Flow** — Database hosting, API deployment, testing environments
- **Nomus Connector** — ERP integration testing, PostgreSQL adapters
- **Inbox Sentinel** — Full SaaS stack deployment and testing
- **PaperclipAI** — Agent execution environments, database hosting

Every SaaS system in the portfolio was prototyped, tested, and initially deployed on this infrastructure before moving to cloud hosting.

---

## License

This is a documentation-only repository describing infrastructure architecture and configuration patterns. No production configuration or credentials are included.

---

**Built by [Alexandre Pereira dos Santos](https://github.com/aleavenger)**
