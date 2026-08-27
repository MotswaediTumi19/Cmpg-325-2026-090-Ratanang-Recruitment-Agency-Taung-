# Physical Topology — Ratanang Recruitment Agency (Taung)

![Physical Topology](../diagrams/physical-topology.svg)

## Devices

| Device | Role | Model (Packet Tracer) |
|---|---|---|
| RTR-TAUNG | Edge router, inter-VLAN routing, Internet gateway | Cisco 4321 (or 2911) |
| ISP-CLOUD | Represents the ISP / Internet | Cloud-PT |
| SW-CORE | Core/distribution switch | Cisco 2960 |
| SW-A | Access switch — Management/Admin + IT/Servers | Cisco 2960 |
| SW-B | Access switch — Recruitment, Client Relations, Printer Zone | Cisco 2960 |
| PC-ADMIN-x | Management/Admin workstations (x8) | PC |
| SRV-FILE, SRV-PRINT | File server, print/DHCP server | Server |
| PC-RECRUIT-x | Recruitment Consultant workstations (x20, represented by a subset in Packet Tracer) | PC |
| PC-CLIENT-x | Client Relations workstations (x15, represented by a subset) | PC |
| PRT-1, PRT-2 | Shared network printers (CR8) | Printer |

## Cabling / Physical Connections

- **RTR-TAUNG Gig0/0 ↔ ISP-CLOUD** — WAN link out to the Internet
- **RTR-TAUNG Gig0/1 ↔ SW-CORE Gig0/1** — trunk carrying all VLANs (router-on-a-stick)
- **SW-CORE Gig0/2 ↔ SW-A Gig0/1** — trunk link
- **SW-CORE Gig0/3 ↔ SW-B Gig0/1** — trunk link
- **SW-A Gig0/2 ↔ SW-B Gig0/2** — redundant trunk link between the two access
  switches

The three switches (SW-CORE, SW-A, SW-B) are cabled in a **triangle**, which is
a deliberate design choice: it gives each access switch two paths back to the
core (direct, and via the other access switch) so a single link or switch
failure does not cut a department off from the router/Internet. This
redundancy is what creates the Layer 2 loop addressed by the assigned STP
challenge — see `logical-topology.md` for the STP design.

- End devices for each department connect to access ports on SW-A or SW-B, as
  shown in the diagram and detailed in the IP addressing plan.

## Physical Placement Notes

- SW-CORE and the servers sit in the IT/Server Room (secure, restricted area).
- SW-A serves the Management/Admin wing of the office.
- SW-B serves the client-facing wing (Recruitment Consultants and Client
  Relations), with the two shared printers physically located there since
  those are the two departments named in CR8.
