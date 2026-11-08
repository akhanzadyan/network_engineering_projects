# Fintech Enterprise Network — High Availability & Security Architecture

I designed and validated a fintech enterprise network integrating headquarter, branch office, remote payment terminals, and redundant Internet connectivity. The architecture uses Cisco Catalyst switching, Palo Alto perimeter firewalls, and Fortinet security appliances to provide resilient connectivity, centralized security enforcement, and segmentation between DMZ, internal users, and application services.

The network uses eBGP multihoming with two Internet providers, preferring the primary ISP through BGP Local Preference for outbound traffic and AS-path prepending toward the secondary ISP for inbound traffic engineering. Remote branche and payment terminals connect through redundant IPsec VPN tunnels, with OSPF costs controlling primary and backup path selection. High availability is implemented through active-passive firewall clusters, monitored interfaces, LACP aggregates across stacked switches, and Rapid PVST+ at branch location.

All documented failover scenarios passed validation, including ISP connectivity failures, firewall hardware and monitored-interface failures, individual LACP member failures without HA takeover, core switch-stack member failures, branch-switch failures with Rapid PVST+ recovery, and IPsec tunnel failover using OSPF. These tests confirmed the intended redundancy and traffic-recovery behavior across the network.

## Network Documentation

- [Network Topology and Design](Fintech-Enterprise-Network-Topology.pdf)
- [Failover and Resiliency Validation](Fintech-Enterprise-Failover-Validation.pdf)
