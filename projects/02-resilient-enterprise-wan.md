# Resilient Enterprise WAN

## Goal
Connect headquarters, branches and data center with resilient routed connectivity.

## Architecture work
Compare hub-spoke and partial mesh; plan summarizable addressing; implement OSPF or BGP as appropriate; document route filters; test link failure, convergence and asymmetric paths.

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
