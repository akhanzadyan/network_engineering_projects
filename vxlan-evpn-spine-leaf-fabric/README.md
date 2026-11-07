# VXLAN EVPN Spine-Leaf Fabric

**Data Center Networking | BGP EVPN | VXLAN | All-Active Multihoming | FortiGate HA**

## Project Overview

Designed, implemented, and validated a redundant data center network based on NVIDIA Cumulus Linux and a two-spine, four-leaf architecture.

The solution integrates BGP EVPN/VXLAN, Ethernet Segment all-active multihoming, LACP, centralized inter-zone routing through FortiGate, and stateful firewall high availability.

## Network Architecture

- **Fabric:** 2 Spine switches and 4 Leaf switches
- **Network OS:** NVIDIA Cumulus Linux
- **Underlay:** eBGP
- **Overlay:** MP-BGP EVPN with VXLAN
- **Redundancy:** ECMP, LACP, and EVPN all-active multihoming
- **Security:** FortiGate Active-Passive HA
- **Endpoints:** 4 Linux hosts

### Network Segmentation

| VLAN  | VXLAN VNI | Subnet | FortiGate Gateway |
|--- |---|---|---|
| 10 | 10010 | 192.168.10.0/24 | 192.168.10.1 |
| 20 | 10020 | 192.168.20.0/24 | 192.168.20.1 |

Each VLAN is extended across the leaf switches using VXLAN, with EVPN providing the control plane.

## Traffic Flow and Security

**Same-VLAN Traffic**

Hosts belonging to the same VLAN communicate through the EVPN/VXLAN fabric without passing through the FortiGate firewall.

**Inter-Zone Traffic**

Traffic between VLAN 10 and VLAN 20 is routed through the FortiGate firewall, where zone-based security policies control communication between the two networks.

FortiGate performs centralized Layer 3 routing and security enforcement.

## High-Availability Architecture

The solution implements redundancy across the network and security layers.

- Redundant spine switches with ECMP forwarding
- EVPN all-active multihoming for dual-attached hosts
- LACP for resilient host and firewall connectivity
- FortiGate Active-Passive HA with session synchronization
- Aggregate interface monitoring for automatic firewall failover
- HA override disabled to prevent unnecessary automatic failback
- Controlled manual failback when operationally required

## Failover and Resiliency Validation

All planned failover tests were completed successfully.

| Test Scenario | Result |
|---|---|
| Same-VLAN connectivity across leaf switches | PASS |
| VXLAN connectivity across the fabric | PASS |
| FortiGate inter-zone routing | PASS |
| Single host LACP member failure | PASS |
| Complete leaf-switch failure | PASS |
| Single spine-switch failure | PASS |
| ECMP path redundancy | PASS |
| Single FortiGate aggregate member failure | PASS |
| FortiGate aggregate connectivity loss | PASS |
| Automatic FortiGate HA failover | PASS |
| FortiGate HA session synchronization | PASS |
| Controlled manual HA failback | PASS |
| End-to-end connectivity following failover | PASS |

The validation demonstrated successful connectivity recovery and redundancy across the fabric, host-access, and firewall layers.
