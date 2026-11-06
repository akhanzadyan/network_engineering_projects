# High availability design for HQ and 3 branches

I designed and tested a production network connecting 3 branches to headquarters. The goal was to restore branch-to-HQ connectivity after a router or circuit failure and maintain HQ Internet access if the active firewall or primary Internet provider failed.

Each branch connects to HQ over 2 provider circuits using route-based IPsec tunnels. IP SLA tracks primary-path reachability so HSRP can move the branch gateway role to the backup router. I tuned EIGRP bandwidth and delay on the backup tunnel interfaces at both ends so traffic normally uses the primary circuit in both directions.

All 6 failover tests passed. They covered the primary branch circuit, active branch router, active HQ router, a Catalyst 9300 core stack member, active ASA firewall, and primary HQ Internet provider.

- [Network topology and design legend](./HQ-Branch-Topology.pdf)
- [Failover scenarios and results](./HQ-Branch-Failover-Results.pdf)
