# CMPG 325 — Individual Semester Project
## Ratanang Recruitment Agency (Taung) — Network Design & Implementation

| Field | Value |
|---|---|
| Student | Motswaedi, Tumi (28128095) |
| Project ID | CMPG325-2026-090 |
| Client ID | CLI-090 |
| Assigned Organisation | Ratanang Recruitment Agency (Taung) |
| Industry | Professional Services |
| Addressing Block | 10.37.0.0/16 (site allocation: 10.37.90.0/24) |
| Technical Challenge | STP — loop prevention & root design (Intermediate) |
| Change Request | CR8 — shared printer zone for two departments that currently cannot print |

## Project Status

- [x] Milestone 1 — Client Design Review (requirements, topology, addressing, repo setup)
- [ ] Milestone 2 — due 2 October 2026
- [ ] Final submission — due 16 October 2026

## Repository Structure

```
RTA-Taung-Network/
├── README.md                       — this file
├── docs/
│   ├── client-requirements.md      — client background, requirements, constraint, CR8
│   ├── physical-topology.md        — physical device layout and cabling
│   ├── logical-topology.md         — VLANs, IP scheme, routing/STP logic
│   └── ip-addressing-plan.md       — full VLSM addressing table
├── diagrams/
│   ├── physical-topology.svg
│   └── logical-topology.svg
└── packet-tracer/
    └── (RTA-Taung-Network.pkt will be added here in Milestone 2)
```

## Design Summary

Ratanang Recruitment Agency is a small professional-services office in Taung with
five functional areas: Management/Admin, Recruitment Consultants, Client Relations,
IT/Server Room, and a shared Printer Zone (introduced by CR8). The network uses a
router-on-a-stick design with three switches — a core switch and two access
switches connected in a triangle — to provide redundant links between wiring
closets. Because the redundant links create a Layer 2 loop, Spanning Tree Protocol
is configured with a deliberately chosen root bridge and secondary root, satisfying
the assigned technical challenge. VLSM is used throughout the addressing plan to
keep subnet sizes matched to actual host counts, in line with the client's
bandwidth constraint.

See `docs/client-requirements.md` for full detail, and `docs/physical-topology.md` /
`docs/logical-topology.md` for the design itself.

## Milestone 2 preview (not yet implemented)

Router, switch and end-device configuration, STP verification evidence,
inter-VLAN ACL for the printer zone, and the working `.pkt` file.
