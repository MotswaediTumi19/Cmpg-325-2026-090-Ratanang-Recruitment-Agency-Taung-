# CMPG 325 — Ratanang Recruitment Agency (Taung)

**Student:** Motswaedi, Tumi (28128095)
**Project ID / Client ID:** CMPG325-2026-090 / CLI-090
**Addressing block:** 10.37.0.0/16 (site network 10.37.90.0/24)
**Technical challenge:** STP — loop prevention and root design
**Change request:** CR8 — shared printer zone (VLAN 50) for Recruitment and Client Relations

## Milestone status
| Milestone | Status |
|---|---|
| 1 — Client design review | Done |
| 2 — Client implementation review | Done |
| 3 | Pending |

## Design summary
Two routers (RTR-TAUNG, ISP-CLOUD), three 2960 switches (SW-CORE, SW-A, SW-B), router-on-a-stick inter-VLAN routing, PAT to the ISP and DHCP for user VLANs. Limited, expensive bandwidth is respected by pruning trunks to the six VLANs in use and disabling CDP on the WAN link.

| VLAN | Name | Subnet | Gateway |
|---|---|---|---|
| 10 | MGMT-ADMIN | 10.37.90.64/28 | 10.37.90.65 |
| 20 | RECRUITMENT | 10.37.90.0/27 | 10.37.90.1 |
| 30 | CLIENT-RELATIONS | 10.37.90.32/27 | 10.37.90.33 |
| 40 | IT-SERVERS | 10.37.90.80/29 | 10.37.90.81 |
| 50 | PRINTER-ZONE | 10.37.90.88/29 | 10.37.90.89 |
| 99 | NATIVE-MGMT | 10.37.90.96/29 | 10.37.90.97 |
| — | WAN | 10.37.90.104/30 | RTR-TAUNG .105 / ISP-CLOUD .106 |

### STP roles
| Switch | Role | Priority |
|---|---|---|
| SW-CORE | Root | 4096 |
| SW-A | Secondary root | 8192 |
| SW-B | Non-root (Gi0/2 to SW-A blocks) | 32768 |

### CR8
Printers PRT-1 (10.37.90.90) and PRT-2 (10.37.90.91) sit in VLAN 50. Two extended ACLs on the router's VLAN 50 subinterface allow traffic only to and from VLANs 20 and 30; VLAN 10, VLAN 40, the management VLAN and the Internet are blocked.

## Milestone 2 deliverables
- Packet Tracer file: `milestone-2/CMPG325-090-Motswaedi-M2.pkt`
- Implementation report: `milestone-2/CMPG325-090-Milestone2-Motswaedi.docx`
- Evidence document: `milestone-2/CMPG325-090-Milestone2-Evidence-Motswaedi.docx`
- Device configurations: `milestone-2/configs/`
- Screenshots T00–T19: `milestone-2/evidence/`

All 18 planned tests (VLANs, trunks, STP root and blocking, PortFast, DHCP, inter-VLAN routing, CR8 allow/deny, ACL counters, PAT, link failure, root failure, recovery) were run in Packet Tracer and passed.
