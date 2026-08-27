# Logical Topology — Ratanang Recruitment Agency (Taung)

![Logical Topology](../diagrams/logical-topology.svg)

## VLAN Design

| VLAN ID | Name | Subnet | Access Switch |
|---|---|---|---|
| 10 | MGMT-ADMIN | 10.37.90.64/28 | SW-A |
| 20 | RECRUITMENT | 10.37.90.0/27 | SW-B |
| 30 | CLIENT-RELATIONS | 10.37.90.32/27 | SW-B |
| 40 | IT-SERVERS | 10.37.90.80/29 | SW-A |
| 50 | PRINTER-ZONE | 10.37.90.88/29 | SW-B |
| 99 | NATIVE-MGMT | 10.37.90.96/29 | all switches |

All inter-switch links (SW-CORE↔RTR, SW-CORE↔SW-A, SW-CORE↔SW-B, SW-A↔SW-B)
are configured as **802.1Q trunks** carrying VLANs 10, 20, 30, 40, 50 and 99.

## Routing

RTR-TAUNG performs inter-VLAN routing using **router-on-a-stick**: one
subinterface per VLAN on Gig0/1, each holding the gateway address for that
VLAN (see the addressing plan). A default route (or NAT/PAT, to be confirmed
in Milestone 2) points out Gig0/0 towards the ISP for Internet-bound traffic.

**CR8 access control:** an access list on the router permits traffic between
VLAN 50 (Printer Zone) and VLAN 20 (Recruitment) / VLAN 30 (Client Relations)
only, and denies VLAN 50 traffic to/from VLAN 10 and VLAN 40. This satisfies
CR8's specific wording — enabling printing for the two named departments —
without opening the printer zone to departments not mentioned in the change
request.

## Spanning Tree Design (assigned technical challenge)

The triangle formed by SW-CORE, SW-A and SW-B is a physical Layer 2 loop once
all three links are trunked. Left unmanaged, this would cause broadcast
storms and duplicate frame delivery. STP is configured as follows:

| Switch | Role | Priority |
|---|---|---|
| SW-CORE | Root bridge (primary) | 4096 |
| SW-A | Secondary root (backup) | 8192 |
| SW-B | Non-root | default (32768) |

- **SW-CORE** is deliberately made the root bridge for all VLANs, since it
  sits closest to the router/Internet edge and should carry the most direct
  paths.
- **SW-A** is configured as the secondary root, so it takes over as root
  automatically if SW-CORE fails.
- With this design, the SW-A↔SW-B redundant link has one end placed into a
  **blocking** state by STP under normal operation (traffic flows via
  SW-CORE), and is only unblocked if a primary link/switch fails —
  preventing the loop while preserving redundancy.
- PortFast + BPDU Guard will be applied to end-device access ports (Milestone
  2) so workstation/printer/server ports don't participate in the spanning
  tree recalculation delay.

Configuration commands, `show spanning-tree` verification output, and
failure-simulation evidence will be captured in Milestone 2.
