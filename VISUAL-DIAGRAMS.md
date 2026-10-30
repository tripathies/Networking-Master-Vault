# Visual Diagrams Library

Mermaid sources are version-controlled and editable. Use draw.io for detailed physical and logical network layouts.

## Enterprise network overview
```mermaid
flowchart TB
 U[Users and endpoints] --> A[Campus / branch access]
 A --> D[Distribution and core]
 D --> E[WAN and security edge]
 E --> I[Internet / SaaS]
 E --> H[Hybrid transit]
 H --> C[Cloud landing zones]
 D --> DC[Data center fabric]
 DC --> APP[Application and data tiers]
 SEC[Identity, firewall policy and monitoring] -. governs .-> A
 SEC -. governs .-> E
 SEC -. governs .-> C
```

## Hybrid cloud connectivity
```mermaid
flowchart LR
 ON[On-premises sites] --> EDGE[Redundant edge routers / firewalls]
 EDGE --> WAN[Private WAN or IPsec VPN]
 WAN --> HUB[Cloud transit hub]
 HUB --> AWS[AWS VPCs]
 HUB --> AZ[Azure VNets]
 HUB --> GCP[GCP VPC networks]
 DNS[Central DNS and IPAM] -. integrates .-> HUB
 MON[Flow logs and monitoring] -. observes .-> HUB
```

## Application delivery
```mermaid
sequenceDiagram
 participant C as Client
 participant D as DNS
 participant E as Edge / WAF / CDN
 participant L as Load balancer
 participant A as Application
 participant DB as Data service
 C->>D: Resolve application name
 D-->>C: Endpoint / traffic policy
 C->>E: HTTPS request
 E->>L: Forward permitted request
 L->>A: Select healthy backend
 A->>DB: Private service request
 DB-->>A: Response
 A-->>C: Application response
```

## Routing decision
```mermaid
flowchart TD
 P[Packet arrives] --> R{Destination local?}
 R -- Yes --> L[Resolve next-hop MAC and deliver]
 R -- No --> T[Look up routing table]
 T --> M{Matching route?}
 M -- Yes --> N[Longest-prefix route and next hop]
 M -- No --> D{Default route?}
 D -- Yes --> N
 D -- No --> X[Drop / unreachable]
 N --> F[Apply forwarding and security policy]
 F --> O[Forward packet]
```

Sources: [architecture.mmd](architecture.mmd), [architecture.drawio](architecture.drawio), [architecture.svg](architecture.svg). Record assumptions, address ranges and security boundaries on every project diagram.
