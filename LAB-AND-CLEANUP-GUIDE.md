# Labs, Validation and Cleanup Guide

## Standard lab record
Capture objective, prerequisites, topology, address plan, platform/version, configuration, expected and observed behavior, validation commands, injected fault, troubleshooting evidence, cleanup and lessons learned.

## Safe lab environments
- Cisco Packet Tracer for introductory switching and routing.
- GNS3, EVE-NG or Containerlab for advanced virtual topologies.
- Linux network namespaces and iproute2 for host networking.
- Wireshark and tcpdump for packet inspection.
- Cloud sandboxes for provider networking, with budgets and teardown checks.

## Validation categories
1. Link and interface state
2. Address, prefix, gateway and ARP/ND correctness
3. Route selection and return path
4. DNS and service reachability
5. Firewall, ACL, security group and network policy behavior
6. MTU, fragmentation and throughput
7. Failover, convergence and recovery
8. Logs, counters, flow telemetry and packet evidence

## Cleanup checklist
- [ ] Remove temporary cloud gateways, VPNs, load balancers and public IPs.
- [ ] Delete temporary VMs, clusters, interfaces, routes and test subnets where safe.
- [ ] Remove test firewall rules and credentials.
- [ ] Confirm no billable resources remain.
- [ ] Sanitize packet captures, logs, screenshots and configuration before committing.
- [ ] Record teardown evidence and retained resources.

Only test networks with explicit authorization. Never store production secrets or sensitive captures here.
