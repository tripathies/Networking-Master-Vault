# OSPF

> **Networking Master Vault · Routing and Layer 3 · NET-05-ospf**

[← Category tracker](../buckets/05-routing-layer3/README.md) · [← Master dashboard](../README.md)

## 1. Fundamentals and purpose

Open Shortest Path First (OSPF) is a link-state Interior Gateway Protocol (IGP). Routers form adjacencies, exchange link-state advertisements (LSAs), build a link-state database and run the Shortest Path First algorithm to calculate routes.

OSPF is commonly used inside an enterprise or service-provider autonomous system. OSPFv2 supports IPv4; OSPFv3 supports IPv6 and has evolved extensions. OSPF uses IP protocol 89, not TCP or UDP ports.

## 2. Key concepts

- **Area 0:** backbone area; non-backbone areas connect to the backbone in a conventional multi-area design.
- **Router ID:** 32-bit identifier, commonly written in IPv4 dotted notation; should be stable and unique within the OSPF domain.
- **Neighbor states:** Down, Init, 2-Way, ExStart, Exchange, Loading and Full (not every network type forms Full adjacency between every pair).
- **LSA:** describes topology or reachability information; type and flooding scope matter.
- **Cost:** interface metric used in path calculation; lower total cost is preferred.
- **DR/BDR:** designated and backup designated routers on eligible multi-access segments; not used on point-to-point links.
- **ABR/ASBR:** area border router connects areas; autonomous system boundary router injects external routes.

## 3. Real-world example

A head office has two distribution routers and several branch routers. OSPF Area 0 runs in the core. Branches may be placed in separate areas if topology and operational scale justify it. Summarize prefixes at area boundaries where possible. Avoid creating areas just for administrative naming; area design changes flooding and troubleshooting complexity.

## 4. Adjacency and packet flow

```mermaid
sequenceDiagram
 participant R1 as Router 1
 participant R2 as Router 2
 R1->>R2: Hello (discover neighbors)
 R2-->>R1: Hello (match parameters)
 R1->>R2: Database Description
 R2-->>R1: Database Description
 R1->>R2: Link State Request
 R2-->>R1: Link State Update
 R1->>R2: Link State Acknowledgment
 Note over R1,R2: LSDB synchronized; adjacency Full where required
```

The control plane builds routes. User data packets are then forwarded using the resulting routing table; OSPF is not in the data path for every packet.

## 5. Cisco IOS / IOS-XE configuration

Example two-router point-to-point lab:
```text
interface gigabitEthernet 0/0
 description R1-TO-R2
 ip address 10.0.12.1 255.255.255.252
 ip ospf 10 area 0
 no shutdown
!
interface loopback 0
 ip address 1.1.1.1 255.255.255.255
!
router ospf 10
 router-id 1.1.1.1
 passive-interface default
 no passive-interface gigabitEthernet 0/0
```

Configure R2 with the peer address `10.0.12.2/30` and a unique router ID. Ensure the loopback is advertised if required; exact advertisement syntax depends on chosen interface-based or network-statement configuration.

**Verification:**
```text
show ip ospf neighbor
show ip ospf interface brief
show ip ospf database
show ip route ospf
show ip protocols
```

Expected: neighbor reaches Full on a point-to-point link, LSDB contains expected LSAs, and learned routes appear with OSPF route codes. If the adjacency is not Full, inspect state and mismatch conditions before changing timers.

## 6. Linux FRRouting example

On a lab Linux router with FRRouting installed, configuration is typically performed in FRR's integrated CLI (`vtysh`), not by ordinary Linux `ip` commands alone:
```text
sudo vtysh
show ip ospf neighbor
show ip route ospf
show ip ospf database
```

Illustrative FRR configuration:
```text
router ospf
 ospf router-id 2.2.2.2
 network 10.0.12.0/30 area 0
```

FRR package, interface and daemon setup varies by distribution. Use the official FRR documentation for the installed version.

## 7. Practical lab: failover and route learning

1. Create R1—R2—R3 in GNS3, EVE-NG or another authorized lab.
2. Use /30 or /31 point-to-point links with unique router IDs.
3. Enable OSPF Area 0 on transit links and advertise loopbacks.
4. Confirm neighbors and learned routes.
5. Ping R3's loopback from R1.
6. Shut one of two alternate paths in the lab and observe route recalculation.
7. Compare routing table and traceroute before and after failure.

**Expected result:** routers learn remote loopback prefixes; when an alternate path exists, traffic reconverges after a link failure. Convergence time depends on timers, topology, implementation and failure detection.

## 8. Cloud implementation comparison

AWS VPC, Azure VNet and Google Cloud VPC do not expose customer-managed OSPF as the ordinary native VPC route-control mechanism. For hybrid connectivity:
- AWS Site-to-Site VPN can support dynamic routing with BGP; Direct Connect commonly uses BGP.
- Azure VPN Gateway and ExpressRoute use BGP for dynamic route exchange in supported designs.
- Google Cloud HA VPN and Cloud Interconnect use Cloud Router with BGP.

Use OSPF inside on-premises networks if appropriate, then exchange routes at the cloud edge using supported BGP designs. Do not assume an OSPF adjacency can be formed directly with a managed cloud gateway.

## 9. Troubleshooting scenarios

- **No neighbor:** verify link, IP subnet, OSPF enabled, area, hello/dead timers, authentication, network type and protocol 89 reachability.
- **Stuck in EXSTART/EXCHANGE:** inspect MTU mismatch, duplicate router ID and database exchange behavior.
- **Neighbor Full but route absent:** inspect LSA scope, area type, filtering, summarization, passive interfaces and route policy.
- **Wrong path selected:** inspect interface costs, ECMP, route preference and more-specific routes.
- **Flapping adjacency:** inspect physical errors, packet loss, CPU, timers and unstable links.

## 10. Interview and design questions

1. Explain OSPF neighbor formation and the path to Full state.
2. What is the difference between an ABR and an ASBR?
3. Why is Area 0 important?
4. Why might an OSPF neighbor remain in EXSTART?
5. How would you connect an OSPF enterprise core to AWS, Azure or GCP without assuming the cloud gateway speaks OSPF?

## Knowledge validation

- [ ] Configure a two-router OSPF adjacency.
- [ ] Read neighbor and LSDB output.
- [ ] Advertise and verify a loopback route.
- [ ] Demonstrate route failover in a controlled lab.
- [ ] Explain OSPF-to-BGP handoff for hybrid cloud.

## Further reading

[RFC 2328 — OSPFv2](https://www.rfc-editor.org/rfc/rfc2328) · [RFC 5340 — OSPFv3](https://www.rfc-editor.org/rfc/rfc5340) · [FRRouting Documentation](https://docs.frrouting.org/) · [AWS Site-to-Site VPN](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html) · [Azure VPN Gateway](https://learn.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways) · [Google Cloud Router](https://cloud.google.com/network-connectivity/docs/router)
