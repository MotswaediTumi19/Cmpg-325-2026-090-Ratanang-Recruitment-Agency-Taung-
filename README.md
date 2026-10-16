# CMPG 325 — Ratanang Recruitment Agency (Taung)

**Student:** Motswaedi, Tumi (28128095) · **Project / Client ID:** CMPG325-2026-090 / CLI-090
**Addressing block:** 10.37.0.0/16 (site network 10.37.90.0/24)
**Technical challenge:** STP — loop prevention and root design
**Change request:** CR8 — shared printer zone (VLAN 50) for Recruitment and Client Relations

## Milestone status
| Milestone | Due | Status |
|---|---|---|
| 1 — Client design review | 28 Aug 2026 | Done |
| 2 — Client implementation review | 2 Oct 2026 | Done |
| Final submission | 16 Oct 2026 | Submitted |

## Final deliverables
| # | Deliverable | Location |
|---|---|---|
| 1 | Packet Tracer project | `final/CMPG325-090-Motswaedi-M2.pkt` (same file also in `milestone-2/`) |
| 2 | GitHub portfolio of evidence | https://github.com/MotswaediTumi19/Cmpg-325-2026-090-Ratanang-Recruitment-Agency-Taung-.git |
| 3 | Technical report | `final/CMPG325-090-Technical-Report-Motswaedi.docx` |
| 4 | 15–20 min inset video demonstration | `final/CMPG325-090-Motswaedi-Demo-Video.mp4` |
| 5 | Additional files | `final/configs/`, `final/evidence/`, `docs/` |

## Repository layout
```
README.md
milestone-1/   client design review documents
milestone-2/   implementation review (pkt, report, evidence doc, configs, screenshots)
final/         technical report, demo video, final .pkt, configs, evidence T00–T19 (final .pkt = milestone-2/…-M2.pkt)
docs/          test log, video run-sheet, submission checklist
```

## Design summary
Two routers (RTR-TAUNG, ISP-CLOUD), three 2960 switches (SW-CORE, SW-A, SW-B), router-on-a-stick inter-VLAN routing, PAT to the ISP and DHCP for user VLANs. Limited, expensive bandwidth is respected by pruning trunks to the six VLANs in use, translating only user ranges and disabling CDP on the WAN link.

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
Printers PRT-1 (10.37.90.90) and PRT-2 (10.37.90.91) sit in VLAN 50. Two extended ACLs on the router's VLAN 50 subinterface allow traffic only to and from VLANs 20 and 30. VLAN 10, VLAN 40, the management VLAN and the Internet are blocked.

## Testing
All 18 tests (T1–T18) passed; see `docs/test-log.md` and screenshots in `final/evidence/`.

## Opening the project
Open the `.pkt` in Cisco Packet Tracer. Console login password is `cisco325` and the enable secret is `Cisco@325` (lab values only).
