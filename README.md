# City Municipality Network

A VLAN-segmented network design for a city municipality, built and simulated
in Cisco Packet Tracer. The network isolates traffic for five departments —
Water, Electricity, Finance, Complaints, and Admin — using VLANs, and
enables inter-VLAN communication through Router-on-a-Stick.

## 1. Introduction

This project designs and implements a secure and efficient network for a
city municipality with five departments: Water, Electricity, Finance,
Complaints, and Admin. The purpose is to isolate department traffic using
VLANs, enable inter-VLAN communication using Router-on-a-Stick, and
automate IP allocation through DHCP. Stakeholders include municipal IT
staff, department managers, and network administrators.

## 2. Background

Modern enterprise and campus networks widely use VLAN segmentation and
Layer 3 routing to optimize traffic flow and enhance security. University
networks, for example, often separate student labs, staff offices, and
administration using VLANs, routing inter-VLAN traffic via central routers.
This design follows Cisco's hierarchical model and best practices to
provide scalability and manageability.

## 3. Network Design

### Devices Used

| Device Type | Model | Quantity | Purpose |
|---|---|---|---|
| Router | 1941 | 1 | Inter-VLAN routing (Router-on-a-Stick) |
| Switch | 2960 | 1 | Layer 2 VLAN switch |
| PCs | PC-PT | 10 | 2 PCs per department |
| Cables | Straight-through | Many | PC-to-switch & switch-to-router connections |

### VLAN / Subnetting Plan

| VLAN | Department | VLAN Name | Network Address | Gateway IP |
|---|---|---|---|---|
| 10 | Water | VLAN_WATER | 192.168.10.0/24 | 192.168.10.1 |
| 20 | Electricity | VLAN_ELEC | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Finance | VLAN_FIN | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Complaints | VLAN_COMP | 192.168.40.0/24 | 192.168.40.1 |
| 50 | Admin | VLAN_ADMIN | 192.168.50.0/24 | 192.168.50.1 |

### Protocols Used

- **VLANs** — to isolate department traffic
- **Router-on-a-Stick** — for inter-VLAN routing over a single physical interface
- **OSPF** — can be added for future dynamic routing
- **DHCP** (optional) — for automatic IP allocation, if required

## 4. Configuration

Full device configurations are in [`configs/`](./configs):

- [`switch-config.txt`](./configs/switch-config.txt) — VLAN creation and access/trunk port assignment
- [`router-config.txt`](./configs/router-config.txt) — Router-on-a-Stick subinterfaces per VLAN

### PC IP Settings (Manual)

| PC | Department | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|---|
| PC0 | Water | 192.168.10.2 | 255.255.255.0 | 192.168.10.1 |
| PC1 | Water | 192.168.10.3 | 255.255.255.0 | 192.168.10.1 |
| PC2 | Electricity | 192.168.20.2 | 255.255.255.0 | 192.168.20.1 |
| PC3 | Electricity | 192.168.20.3 | 255.255.255.0 | 192.168.20.1 |
| PC4 | Finance | 192.168.30.2 | 255.255.255.0 | 192.168.30.1 |
| PC5 | Finance | 192.168.30.3 | 255.255.255.0 | 192.168.30.1 |
| PC6 | Complaints | 192.168.40.2 | 255.255.255.0 | 192.168.40.1 |
| PC7 | Complaints | 192.168.40.3 | 255.255.255.0 | 192.168.40.1 |
| PC8 | Admin | 192.168.50.2 | 255.255.255.0 | 192.168.50.1 |
| PC9 | Admin | 192.168.50.3 | 255.255.255.0 | 192.168.50.1 |

## 5. Testing

- Ping `192.168.X.1` from each PC to verify default gateway reachability
- Inter-VLAN ping tests (e.g., PC0 → PC5) to confirm Router-on-a-Stick is working correctly

```
ping 192.168.X.X
```

## 6. Conclusion

This project demonstrates the implementation of a structured network using
VLANs and Router-on-a-Stick routing. The design improves security by
segmenting departments and enhances scalability for future expansion. The
approach is cost-effective, follows industry standards, and supports
municipal operations efficiently.

## Repository Contents

```
city-municipality-network/
├── README.md                          → this project report
├── LICENSE
├── configs/
│   ├── switch-config.txt              → VLAN + port configuration
│   └── router-config.txt              → Router-on-a-Stick subinterfaces
├── docs/
│   └── lab-manual.md                  → step-by-step build guide
└── packet-tracer/
    └── city-municipality-network.pkt  → the Packet Tracer simulation file
```

## How to Use

1. Open [`packet-tracer/city-municipality-network.pkt`](./packet-tracer/city-municipality-network.pkt) in Cisco Packet Tracer to explore the live topology.
2. Follow [`docs/lab-manual.md`](./docs/lab-manual.md) to rebuild the network from scratch.
3. Reference [`configs/`](./configs) for the exact CLI commands used on the switch and router.

## Tech

- Cisco Packet Tracer
- Cisco IOS CLI (VLANs, trunking, Router-on-a-Stick, subinterfaces)


## Publication copy

Published 5 October 2026 at the owner's request. This is a sanitized source snapshot. Original local Git history and original files remain unchanged. Pictures, videos, binary archives, private/runtime data, dependency folders and credentials are excluded. Notebook outputs, attachments and incidental metadata are removed. Documents are text-only extracts. Media references and redacted configuration may need replacements before running. No claim of successful rerun, production readiness, sole authorship or independent validation is implied.

Existing GitHub work checked and sanitized. Any supplied attribution is retained. Runtime operation not verified here.
