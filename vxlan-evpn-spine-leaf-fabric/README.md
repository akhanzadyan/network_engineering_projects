# VXLAN EVPN Spine-Leaf Fabric

**Data Center Networking | BGP EVPN | VXLAN | All-Active Multihoming | FortiGate HA**


I designed and tested a data center network using a 2-spine, 4-leaf architecture with NVIDIA Cumulus Linux. The goal was to provide resilient host connectivity, maintain network availability during link or switch failures, and ensure inter-zone connectivity during firewall failover.

The fabric uses eBGP for the underlay and MP-BGP EVPN/VXLAN for the overlay. I implemented EVPN all-active multihoming with LACP for redundant host and firewall connectivity across leaf switches. A FortiGate Active-Passive HA cluster provides centralized inter-zone routing and security enforcement, with session pickup enabled to support stateful failover.

All failover tests passed. They covered individual LACP member failures, complete leaf and spine switch failures, ECMP path redundancy, FortiGate aggregate link failures, automatic firewall HA failover, and controlled manual failback.

## Network Documentation

- [Network Topology and Design](VXLAN-EVPN-Topology.pdf)
- [Failover and Resiliency Validation — All 12 Tests Passed](VXLAN-EVPN-Failover-Results.pdf)
