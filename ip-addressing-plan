# IP Addressing Plan — Ratanang Recruitment Agency (Taung)

## Allocation Approach

Assigned block: **10.37.0.0/16**

Client ID is CLI-090, so the site network is drawn from **10.37.90.0/24**
(third octet = client number), leaving the rest of the /16 free for other
client sites in the wider organisation-level address space. Within the
/24, VLSM is used so each subnet is sized to its actual host count —
this directly supports the client's "minimise waste" constraint, since no
subnet is larger than it needs to be and the majority of the /24
(10.37.90.108 – 10.37.90.255) is left unused/reserved for future growth.

## VLSM Table

| VLAN | Department | Hosts needed | Subnet | Mask | Usable range | Broadcast | Gateway (router subinterface) |
|---|---|---|---|---|---|---|---|
| 20 | Recruitment Consultants | 20 | 10.37.90.0/27 | 255.255.255.224 | .1 – .30 | .31 | 10.37.90.1 |
| 30 | Client Relations | 15 | 10.37.90.32/27 | 255.255.255.224 | .33 – .62 | .63 | 10.37.90.33 |
| 10 | Management/Admin | 8 | 10.37.90.64/28 | 255.255.255.240 | .65 – .78 | .79 | 10.37.90.65 |
| 40 | IT / Server Room | 6 | 10.37.90.80/29 | 255.255.255.248 | .81 – .86 | .87 | 10.37.90.81 |
| 50 | Shared Printer Zone (CR8) | 2 | 10.37.90.88/29 | 255.255.255.248 | .89 – .94 | .95 | 10.37.90.89 |
| 99 | Switch Management (native) | 3 | 10.37.90.96/29 | 255.255.255.248 | .97 – .102 | .103 | 10.37.90.97 |
| — | Router-to-ISP WAN link | 2 | 10.37.90.104/30 | 255.255.255.252 | .105 – .106 | .107 | n/a (point-to-point) |
| — | Reserved for growth | — | 10.37.90.108/29 – 10.37.90.248/29 | — | — | — | unused |

*(Note: in a real deployment the WAN interface address is normally provided
by the ISP rather than drawn from the client's private block; a /30 from the
internal block is used here only so the link can be fully addressed inside
Packet Tracer.)*

## Device-to-Subnet Assignment

- **VLAN 10** (Management/Admin): Director, HR, finance and reception PCs
- **VLAN 20** (Recruitment Consultants): consultant workstations
- **VLAN 30** (Client Relations): account manager workstations
- **VLAN 40** (IT/Servers): file/print server, IT admin PC
- **VLAN 50** (Shared Printer Zone): the two shared network printers (CR8)
- **VLAN 99**: switch management interfaces (SW-CORE, SW-A, SW-B)

## Routing Notes

- Inter-VLAN routing is performed by the edge router using router-on-a-stick
  (one subinterface per VLAN on the link to the core switch).
- By default, all VLANs can reach each other and the Internet through the
  router. An access list restricts VLAN 50 (printer zone) so that only VLAN 20
  and VLAN 30 traffic is permitted to/from it, per CR8's specific wording —
  full ACL configuration will be documented in Milestone 2.
