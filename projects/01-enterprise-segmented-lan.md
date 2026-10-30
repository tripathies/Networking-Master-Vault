# Enterprise Segmented LAN

## Goal
Design a campus LAN with user, server, voice, guest and management segments.

## Architecture work
Create VLAN/IP plan; configure access and trunk links; enable inter-VLAN routing; apply least-privilege ACLs; validate DHCP/DNS; test permitted and denied flows; test redundant uplinks.

## Deliverables
- [ ] Requirements, assumptions and constraints
- [ ] Logical and physical topology diagrams
- [ ] IP addressing and routing plan
- [ ] Security zones and allowed-flow matrix
- [ ] Configuration or infrastructure-as-code source
- [ ] Validation plan with expected results
- [ ] Controlled failure and recovery test
- [ ] Monitoring dashboard and operations runbook
- [ ] Sanitized evidence and cleanup record

## Design review questions
1. What are the trust boundaries and failure domains?
2. How does the return path work?
3. How are DNS, identity and certificates handled?
4. What happens when a link, node, region or provider fails?
5. How will changes be reviewed, rolled back and audited?
