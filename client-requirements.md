# Client Requirements — Ratanang Recruitment Agency (Taung)

## 1. Client Background

Ratanang Recruitment Agency is a small professional-services business operating
from a single office in Taung. The agency places candidates with employer
clients, which means most staff spend their day on phone/video calls, CRM-style
record keeping, and document handling (CVs, contracts, placement letters).

## 2. Functional Areas (assumed departmental scenario)

Since the brief does not itemise departments, the following reasonable
breakdown is used as the basis for the design, sized for a small single-site
agency:

| Department | Approx. users/devices | Role |
|---|---|---|
| Management & Administration | 8 | Director, HR, finance, reception |
| Recruitment Consultants | 20 | Candidate sourcing, interviews, CRM use |
| Client Relations | 15 | Employer accounts, placements, contracts |
| IT & Server Room | 6 | File/print server, local IT admin |
| Shared Printer Zone (CR8) | 2 printers | Shared printing for two departments |

## 3. Client-Stated Requirements

- Assigned organisation: Ratanang Recruitment Agency (Taung)
- Industry: Professional Services
- Assigned addressing block: **10.37.0.0/16**
- Provide appropriate connectivity and network services for the scenario
- Accommodate the stated design constraint and change request
- Produce a working, testable Cisco Packet Tracer implementation

## 4. Design Constraint

> Internet bandwidth is limited and expensive — design must minimise waste.

Implications for the design:
- Subnets are sized to actual host counts using VLSM rather than flat /24s per
  department, so no address space (and no unnecessarily large broadcast domain)
  is wasted.
- Departments are split into separate VLANs so broadcast traffic from one
  department does not consume switching/WAN capacity intended for another.
- No unnecessary services are pushed to the WAN link; inter-VLAN traffic stays
  local to the router, and only genuine Internet-bound traffic exits via the
  edge router.

## 5. Assigned Technical Challenge

**STP — loop prevention & root design (Intermediate)**

The physical design intentionally includes a redundant link between the two
access switches (in addition to their links to the core switch), so that a
single switch or uplink failure does not isolate a department. This redundancy
creates a Layer 2 loop, which is resolved with Spanning Tree Protocol:
- The core switch is configured as the primary root bridge (lowest priority).
- One access switch is configured as the secondary root (backup).
- STP blocks the redundant link under normal conditions and only unblocks it if
  the primary path fails.

Full configuration and verification evidence will be added in Milestone 2.

## 6. Change Request

**CR8: A shared printer zone must serve two departments that currently cannot
print.**

The two departments affected are **Recruitment Consultants** and **Client
Relations** — the two client-facing departments that generate the most
printed material (CVs, contracts, placement letters) but do not currently have
printer access. The design adds a Shared Printer Zone (VLAN 50) physically
located on the same access switch as these two departments, with routing
permitted only between VLAN 50 and these two VLANs. Per the brief's
instruction to follow the specific wording of the change request rather than
introduce additional scope, Management/Admin and IT are **not** given access to
this printer zone as part of CR8 — they are assumed to already have their own
printing arrangement.

## 7. Out of Scope

- Wireless networking (not requested in the brief)
- Voice/video services
- Any department or service not listed above
