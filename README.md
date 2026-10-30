# Networking Master Vault

> **Vendor-neutral Networking Solution Architect learning portal** — build networking fundamentals, design enterprise and hybrid networks, complete practical labs, and track every topic from fundamentals to architecture.

[![Learning tracker](https://img.shields.io/badge/Learning%20tracker-100%20topics-0EA5E9?style=for-the-badge)](#networking-learning-tracker)
[![Reference architecture](https://img.shields.io/badge/Reference%20architecture-open%20design-107C10?style=for-the-badge)](NETWORK-REFERENCE-ARCHITECTURE.md)
[![Visual library](https://img.shields.io/badge/Diagrams-SVG%20%7C%20Mermaid-7F56D9?style=for-the-badge)](VISUAL-DIAGRAMS.md)

## Start here

| 📚 Learning tracker | 🏗️ Enterprise design | 🗺️ Visual library |
|---|---|---|
| Work through 10 domains and 100 linked component guides. | Understand campus, data center, WAN, cloud, hybrid and multi-cloud patterns. | Explore editable Mermaid and draw.io architecture sources. |
| [Open the tracker ↓](#networking-learning-tracker) | [Open reference architecture →](NETWORK-REFERENCE-ARCHITECTURE.md) | [Open diagrams →](VISUAL-DIAGRAMS.md) |

## Networking learning tracker

**Catalogue:** 100 component and concept guides across 10 domains. Every topic links to its dedicated guide and every domain has its own checklist.

| ID | Domain | Topics | Category tracker |
|---|---|---:|---|
| 01 | [Core Networking Fundamentals](buckets/01-core-fundamentals/README.md) | 10 | [Open tracker](buckets/01-core-fundamentals/README.md) |
| 02 | [Network Devices and Infrastructure](buckets/02-network-devices/README.md) | 10 | [Open tracker](buckets/02-network-devices/README.md) |
| 03 | [IP Addressing and Subnetting](buckets/03-ip-addressing/README.md) | 10 | [Open tracker](buckets/03-ip-addressing/README.md) |
| 04 | [Switching and Layer 2](buckets/04-switching-layer2/README.md) | 10 | [Open tracker](buckets/04-switching-layer2/README.md) |
| 05 | [Routing and Layer 3](buckets/05-routing-layer3/README.md) | 10 | [Open tracker](buckets/05-routing-layer3/README.md) |
| 06 | [Transport Protocols and Network Services](buckets/06-protocols-services/README.md) | 10 | [Open tracker](buckets/06-protocols-services/README.md) |
| 07 | [Network Security](buckets/07-network-security/README.md) | 10 | [Open tracker](buckets/07-network-security/README.md) |
| 08 | [Cloud and Hybrid Networking](buckets/08-cloud-hybrid/README.md) | 10 | [Open tracker](buckets/08-cloud-hybrid/README.md) |
| 09 | [Containers and Traffic Distribution](buckets/09-containers-traffic/README.md) | 10 | [Open tracker](buckets/09-containers-traffic/README.md) |
| 10 | [Network Operations and Architecture](buckets/10-operations-architecture/README.md) | 10 | [Open tracker](buckets/10-operations-architecture/README.md) |

## Five learning pillars

1. **Core fundamentals** — understand how hosts, frames, packets, protocols and links work.
2. **Network infrastructure** — understand switching, routing, wireless and physical components.
3. **Cloud and hybrid connectivity** — apply networking principles to AWS, Azure, GCP and on-premises environments.
4. **Containers and traffic distribution** — connect workloads, services, clusters, edges and users.
5. **Security and performance** — protect traffic, observe behavior, troubleshoot and design for resilience.

## Learning method

For each topic follow the same loop:

**Understand the purpose → inspect the architecture → study packet/traffic flow → configure a lab → validate expected behavior → break and troubleshoot → document trade-offs.**

The category checklists are manual GitHub Markdown checklists; they do not synchronize progress or calculate a live personal completion percentage. Use a personal fork or branch to maintain your own checklist state.

## Portfolio projects

- [Enterprise segmented LAN](projects/01-enterprise-segmented-lan.md)
- [Resilient routed enterprise WAN](projects/02-resilient-enterprise-wan.md)
- [Hybrid multi-cloud network](projects/03-hybrid-multicloud-network.md)
- [Kubernetes platform networking](projects/04-kubernetes-platform-networking.md)
- [Secure zero-trust network](projects/05-secure-zero-trust-network.md)
- [Global application delivery](projects/06-global-application-delivery.md)

## Architecture and operations

- [Network reference architecture](NETWORK-REFERENCE-ARCHITECTURE.md)
- [Visual diagrams library](VISUAL-DIAGRAMS.md)
- [Learning roadmap](LEARNING-ROADMAP.md)
- [Labs and validation guide](LAB-AND-CLEANUP-GUIDE.md)
- [Sources and official documentation](SOURCES.md)

## Lab safety

- Use isolated labs, emulators or explicitly authorized environments.
- Never scan, capture or modify networks without permission.
- Do not commit passwords, private keys, VPN profiles, tokens, production IP inventories or packet captures containing sensitive data.
- Use synthetic addressing and sanitized configurations in portfolio material.
- Check licensing and resource requirements before running virtual network appliances.
