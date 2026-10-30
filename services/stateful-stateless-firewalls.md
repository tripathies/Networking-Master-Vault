# Stateful and Stateless Firewalls

> **Networking Master Vault · Network Security · NET-07-stateful-stateless-firewalls**

[← Category tracker](../buckets/07-network-security/README.md) · [← Master dashboard](../README.md)

## 1. Fundamentals and purpose

A firewall enforces traffic policy at a network boundary or workload interface.

- **Stateless filtering** evaluates each packet against rules such as source/destination address, protocol, port and direction. It does not inherently track connection state.
- **Stateful inspection** maintains connection/session state. Return traffic for an allowed session can be permitted based on the connection table, subject to implementation and policy.
- **Next-generation firewalls** may add application identification, user identity, intrusion prevention, TLS inspection and threat intelligence.

A stateful firewall is not automatically secure by default. Policy design, rule order, default behavior, logging, high availability and change governance matter.

## 2. Real-world policy example

A three-tier application has web, application and database segments:
- Internet → web tier: TCP 443 only, via WAF/edge controls.
- Web tier → app tier: only required application port.
- App tier → database: only database listener port.
- Admin network → management interfaces: restricted privileged access.
- Database → internet: deny by default unless a documented dependency requires egress.

Use explicit source/destination objects and service definitions. Avoid broad any-any rules. Document owner, purpose, ticket, expiry and review date.

## 3. Packet and session flow

```mermaid
sequenceDiagram
 participant C as Client
 participant FW as Stateful Firewall
 participant S as Server
 C->>FW: TCP SYN to server:443
 FW->>FW: Evaluate policy; create session state
 FW->>S: Forward SYN
 S-->>FW: SYN-ACK
 FW->>FW: Match reverse packet to session
 FW-->>C: Forward SYN-ACK
 C->>FW: ACK / HTTPS data
 FW->>S: Forward established flow
```

Stateless ACLs may require explicit rules for both directions and ephemeral return traffic. Stateful session tracking simplifies return-flow policy but can be affected by asymmetric routing and state synchronization.

## 4. Cisco ACL examples

Cisco IOS ACLs are packet filters and are not equivalent to every commercial stateful firewall feature.

**Extended ACL example:**
```text
ip access-list extended WEB-IN
 permit tcp 192.0.2.0 0.0.0.255 host 198.51.100.10 eq 443
 deny ip any any log
!
interface gigabitEthernet 0/0
 ip access-group WEB-IN in
!
show access-lists
show ip interface gigabitEthernet 0/0
```

Rule order matters; implicit deny exists at the end of an ACL. Validate direction and interface placement before applying.

## 5. Linux nftables example

Run only in a disposable VM/namespace with console access; a bad firewall change can disconnect a host.

```bash
sudo nft list ruleset
```

Illustrative baseline (adapt and test; do not paste into a production host):
```text
table inet filter {
 chain input {
  type filter hook input priority 0; policy drop;
  iif lo accept
  ct state established,related accept
  ip protocol icmp accept
  tcp dport 22 ip saddr 192.0.2.0/24 accept
 }
}
```

Expected: loopback and established traffic are allowed; SSH is allowed only from the specified documentation subnet; other inbound traffic is dropped. Actual SSH access requires correct interface, routing and daemon configuration.

## 6. Practical lab: enforce three-tier segmentation

1. Create client, web, app and database segments in a lab.
2. Define the approved flow matrix.
3. Apply a default-deny policy at the firewall.
4. Permit only required ports between tiers.
5. Test allowed HTTPS and app-to-database traffic.
6. Test denied direct client-to-database traffic.
7. Inspect session table, counters and logs.
8. Introduce asymmetric routing in a controlled lab and observe stateful session failure.

**Expected result:** only explicitly permitted flows succeed. A successful TCP connection should be visible in session state/logs; denied traffic should match the intended deny rule.

## 7. Cloud comparison

| Capability | AWS | Azure | Google Cloud |
|---|---|---|---|
| Workload stateful control | Security Groups are stateful | NSGs are stateful | VPC firewall rules are stateful |
| Stateless subnet filtering | Network ACLs are stateless | NSGs are stateful; Azure Firewall is stateful; use supported network appliances for stateless needs | VPC firewall rules are stateful; Cloud NGFW adds advanced controls |
| Central inspection | AWS Network Firewall / third-party appliances | Azure Firewall / NVA | Cloud NGFW / third-party appliances |
| Analysis | VPC Flow Logs, Reachability Analyzer | Network Watcher, NSG diagnostics/flow logs | VPC Flow Logs, Connectivity Tests, firewall logs |

Cloud security constructs differ in rule evaluation, scope and logging. Read provider-specific behavior rather than assuming all network controls are interchangeable with a physical firewall ACL.

## 8. Troubleshooting scenarios

- **SYN reaches firewall but no SYN-ACK:** inspect server listener, route, host firewall and return path.
- **One direction works:** check asymmetric routing and state table placement.
- **Rule appears correct but traffic denied:** verify rule order, direction, object expansion, NAT stage and zone policy.
- **Established sessions drop during failover:** check state synchronization, routing convergence and session persistence.
- **Unexpected allowed traffic:** inspect broad rules, security group references, inherited policies and default behavior.

## 9. Interview and architecture questions

1. Explain stateful vs stateless filtering with a TCP handshake.
2. Why can asymmetric routing break stateful inspection?
3. Compare AWS Security Groups and Network ACLs.
4. How would you design east-west segmentation for a three-tier application?
5. What evidence is required before changing a production firewall rule?

## 10. Knowledge validation

- [ ] Write and verify a least-privilege ACL.
- [ ] Demonstrate connection tracking in nftables or a lab firewall.
- [ ] Build a flow matrix and test allowed/denied traffic.
- [ ] Explain state synchronization and asymmetric routing.
- [ ] Compare AWS, Azure and GCP network policy constructs accurately.

## Further reading

[Netfilter / nftables](https://netfilter.org/projects/nftables/) · [AWS Security Groups and NACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html) · [Azure NSGs](https://learn.microsoft.com/azure/virtual-network/network-security-groups-overview) · [Google Cloud firewall rules](https://cloud.google.com/firewall/docs/firewalls)
