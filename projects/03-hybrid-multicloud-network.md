# Hybrid Multi-Cloud Network

## Goal
Connect on-premises networks to AWS, Azure and Google Cloud using controlled transit.

## Architecture work
Create non-overlapping CIDRs; design hub-and-spoke transit; compare IPsec VPN and dedicated connectivity; define DNS resolution; control route propagation; validate private service paths.

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
