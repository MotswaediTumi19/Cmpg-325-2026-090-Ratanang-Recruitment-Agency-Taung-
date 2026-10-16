# Test log (T1–T18)
| ID | Test | Expected | Result | Evidence |
|---|---|---|---|---|
| T1 | VLANs present | 6 VLANs on SW-A/SW-B, correct ports | Pass | T01-vlans-SW-A/B |
| T2 | Trunks | native 99, allowed 10,20,30,40,50,99 | Pass | T02-trunks-* |
| T3 | Root bridge | SW-CORE is root | Pass | T03 |
| T4 | Secondary root | SW-A priority 8212 | Pass | T04 |
| T5 | Loop blocked | SW-B Gi0/2 Altn BLK | Pass | T05, T05b |
| T6 | PortFast/BPDU Guard | portfast on access ports | Pass | T06-* |
| T7 | Router subinterfaces | up/up | Pass | T07 |
| T8 | DHCP | leases with correct gateway | Pass | T08-* |
| T9 | Inter-VLAN | REC to CLI replies | Pass | T09 |
| T10 | CR8 allowed REC | reaches printers | Pass | T10 |
| T11 | CR8 allowed CLI | reaches printers | Pass | T11 |
| T12 | CR8 blocked ADM | unreachable | Pass | T12 |
| T13 | CR8 blocked IT | unreachable | Pass | T13 |
| T14 | ACL counters | permit/deny matches | Pass | T14 |
| T15 | PAT/Internet | 8.8.8.8 reachable | Pass | T15-* |
| T16 | Link failure | reconverges, 5/339 lost | Pass | T16-* |
| T17 | Root failure | SW-A becomes root | Pass | T17-* |
| T18 | Recovery | SW-CORE root again | Pass | T18-* |
