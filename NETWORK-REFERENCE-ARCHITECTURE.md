# Enterprise Network Reference Architecture

## Architecture intent
A vendor-neutral reference model for secure, segmented and resilient enterprise networking across campus, branch, data center, WAN, public cloud and remote users.

## Logical zones
1. **Endpoints:** managed clients, mobile, IoT and guest devices.
2. **Campus/branch access:** wired access, Wi-Fi, access switching and segmentation.
3. **Distribution/core:** Layer 3 boundaries, route summarization and resilient paths.
4. **WAN/edge:** ISP, SD-WAN or routed WAN, edge firewalls and DDoS controls.
5. **Data center:** leaf-spine fabric, workload segments, load balancers and shared services.
6. **Cloud landing zones:** AWS VPC, Azure VNet and Google Cloud VPC with explicit routes and trust boundaries.
7. **Hybrid transit:** VPN or dedicated connectivity, transit hubs, route control and DNS integration.
8. **Application delivery:** DNS, global traffic management, CDN, WAF and regional load balancers.
9. **Security/operations:** identity-aware access, policy enforcement, logs, flow telemetry, packet analysis and automation.

## Design principles
- Use hierarchical, summarizable IP plans; avoid overlapping CIDRs across sites and clouds.
- Separate environments and trust zones; permit only documented flows.
- Use dynamic routing where scale and convergence justify it; control redistribution and route propagation.
- Design predictable return paths, especially around stateful firewalls and NAT.
- Build redundancy across independent failure domains and test failover.
- Use private connectivity for sensitive paths where justified; encrypt traffic over untrusted networks.
- Centralize DNS, time, telemetry and configuration standards.
- Apply least privilege to network administration and automate reviewed changes.
- Measure availability, latency, jitter, loss, throughput, utilization and user experience.

## Architecture decisions
| Decision | Questions |
|---|---|
| Addressing | IPv4/IPv6, CIDR allocation, overlap avoidance and IPAM ownership? |
| Segmentation | Which trust zones, VLANs, VRFs, subnets and policies? |
| Routing | Static/dynamic, BGP/OSPF boundaries, filtering and failover? |
| Connectivity | Internet, VPN, private circuits, peering or transit hub? |
| Security | Firewall placement, identity, inspection, egress and DDoS? |
| Delivery | DNS, CDN, WAF, L4/L7 load balancing and health checks? |
| Resilience | Failure domains, convergence and tested recovery? |
| Operations | Telemetry, change control, automation and runbooks? |

## Cloud service mapping
- **AWS:** VPC, subnets, route tables, internet/NAT gateways, Transit Gateway, Site-to-Site VPN, Direct Connect, Route 53 and ELB.
- **Azure:** VNet, subnets, UDRs, NSGs, Azure Firewall, Virtual WAN, VPN Gateway, ExpressRoute, Private Link and Azure DNS.
- **GCP:** VPC networks, subnets, routes, firewall policies, Cloud NAT, Cloud VPN, Cloud Interconnect, Network Connectivity Center, Cloud DNS and Cloud Load Balancing.

Validate current features, regional availability, quotas, limits and pricing against official documentation before implementation.

## Review checklist
- [ ] IP plan and ownership documented
- [ ] Segmentation and allowed flows approved
- [ ] Routing and return paths validated
- [ ] Redundancy and failover tested
- [ ] DNS, certificates and time dependencies reviewed
- [ ] Security inspection and egress controls tested
- [ ] Monitoring, alerting and runbooks implemented
- [ ] IaC and configuration changes peer-reviewed
- [ ] Cost, capacity and lifecycle ownership assigned
