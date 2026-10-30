# 03. IP Addressing and Subnetting

> Category tracker · 10 topics · Networking Master Vault

[← Back to master dashboard](../../README.md) · [Open reference architecture](../../NETWORK-REFERENCE-ARCHITECTURE.md)

## Category architecture diagram

![03-ip-addressing architecture](diagrams/category-architecture.svg)

- [Open editable draw.io source](diagrams/category-architecture.drawio)
- [View SVG preview](diagrams/category-architecture.svg)

Use the editable diagram as the category-level reference. Extend it with environment-specific addressing, trust boundaries, routing, redundancy and operational ownership when building a real design.

## Learning checklist

- [ ] [IPv4 Addressing](../../services/ipv4.md) — 32-bit addressing, private ranges and special-use addresses.
- [ ] [IPv6 Addressing](../../services/ipv6.md) — 128-bit addressing, global unicast, link-local, multicast and address planning.
- [ ] [Subnet Masks and Network Boundaries](../../services/subnet-masks.md) — Identify network and host portions of an IPv4 address.
- [ ] [CIDR and Prefix Lengths](../../services/cidr.md) — Represent network ranges efficiently with prefix notation.
- [ ] [IPv4 Subnetting](../../services/subnetting.md) — Calculate network, broadcast, usable host range and subnet capacity.
- [ ] [VLSM and FLSM](../../services/vlsm.md) — Allocate variable or fixed-size subnets to match address requirements.
- [ ] [Enterprise IP Address Planning](../../services/ip-address-planning.md) — Design scalable, summarizable address plans across sites, environments and tenants.
- [ ] [Public and Private IP Addressing](../../services/public-private-ip.md) — Understand routability, private ranges and address translation.
- [ ] [Static and Dynamic Address Assignment](../../services/static-dynamic-ip.md) — Choose manual, reservation or dynamically leased host addressing.
- [ ] [IP Address Management (IPAM)](../../services/ipam.md) — Track address allocation, ownership, utilization, DNS and DHCP relationships.

## Completion standard

A topic is complete when you can explain its purpose and trade-offs, draw its traffic flow, configure or inspect it in a safe lab, validate expected behavior, troubleshoot one failure, and explain where it fits in an enterprise design.

## Suggested lab evidence

Record objective, topology, addressing, configuration, expected result, observed result, failure injection, troubleshooting steps, screenshots or sanitized command output, cleanup and lessons learned.
