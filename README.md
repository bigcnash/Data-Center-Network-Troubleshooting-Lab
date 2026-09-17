# Data Center Network Redundancy & Troubleshooting Lab

## Project Overview

This project simulates a redundant data center network built in Cisco Packet Tracer using a Layer 3 spine-leaf architecture.

The environment includes segmented web, application, database, and management networks connected through redundant spine switches. OSPF was configured across the routed fabric to provide dynamic route exchange and automatic path failover.

After validating normal connectivity, the LEAF-01 to SPINE-01 uplink was intentionally disabled to simulate a network failure. OSPF detected the topology change and automatically rerouted traffic through SPINE-02 while maintaining end-to-end connectivity between the web and application networks.

The failed link was then restored, the OSPF adjacency re-formed, and the network returned to its normal redundant state.
![Final Data Center Topology](01-final-datacenter-topology.png)

## Skills Demonstrated

- Data Center Networking
- Spine-Leaf Architecture
- Cisco IOS
- Layer 2 and Layer 3 Switching
- VLAN Configuration
- Inter-VLAN Routing
- IP Addressing and Subnetting
- OSPF Dynamic Routing
- Network Redundancy
- Route Failover
- Network Troubleshooting
- Connectivity Verification
## Network Architecture

The lab uses a redundant spine-leaf design consisting of:

- 1 Edge Router
- 2 Spine Layer 3 Switches
- 2 Leaf Layer 3 Switches
- 2 Web Servers
- 1 Application Server
- 1 Database Server
- 1 Administrative Workstation

Each leaf switch maintains a routed connection to both spine switches. OSPF provides dynamic route exchange and allows traffic to automatically move to the remaining spine path if an uplink fails.

## VLAN and Server Networks

| VLAN | Purpose | Network | Gateway | Devices |
|---|---|---|---|---|
| 10 | Web Servers | 192.168.10.0/24 | 192.168.10.1 | WEB-01, WEB-02 |
| 20 | Application | 192.168.20.0/24 | 192.168.20.1 | APP-01 |
| 30 | Database | 192.168.30.0/24 | 192.168.30.1 | DB-01 |
| 99 | Management | 192.168.99.0/24 | 192.168.99.1 | ADMIN-PC |

## Endpoint Addressing

| Device | IP Address | Default Gateway |
|---|---|---|
| WEB-01 | 192.168.10.11 | 192.168.10.1 |
| WEB-02 | 192.168.10.12 | 192.168.10.1 |
| APP-01 | 192.168.20.11 | 192.168.20.1 |
| DB-01 | 192.168.30.11 | 192.168.30.1 |
| ADMIN-PC | 192.168.99.10 | 192.168.99.1 |

## Routed Fabric

| Connection | Network |
|---|---|
| EDGE-RTR ↔ SPINE-01 | 10.0.0.0/30 |
| EDGE-RTR ↔ SPINE-02 | 10.0.0.4/30 |
| SPINE-01 ↔ LEAF-01 | 10.0.1.0/30 |
| SPINE-01 ↔ LEAF-02 | 10.0.1.4/30 |
| SPINE-02 ↔ LEAF-01 | 10.0.1.8/30 |
| SPINE-02 ↔ LEAF-02 | 10.0.1.12/30 |

## Network Verification

After configuring the routed fabric, VLANs, gateways, and OSPF, connectivity was verified across the data center.

### OSPF Redundancy

LEAF-01 successfully formed OSPF adjacencies with both spine switches, providing two available Layer 3 paths through the data center fabric.

![OSPF Redundant Neighbors](02-ospf-redundancy.png)

### Cross-Fabric Connectivity

Connectivity was tested from WEB-01 to APP-01 across the routed spine-leaf fabric.

The test returned four successful replies with 0% packet loss.

![Cross Fabric Connectivity](03-cross-fabric-connectivity.png)

## Failure Simulation and Troubleshooting

To test network resiliency, the uplink between LEAF-01 and SPINE-01 was intentionally shut down.

Before the failure, traffic from WEB-01 to APP-01 followed the SPINE-01 path:

```text
WEB-01
→ LEAF-01
→ SPINE-01
→ LEAF-02
→ APP-01
```
## Conclusion
This project demonstrated the design, configuration, validation, and troubleshooting of a redundant data center network.

The environment used a spine-leaf architecture with Layer 3 routed uplinks, VLAN segmentation, inter-VLAN routing, and OSPF dynamic routing. Connectivity was verified between web, application, database, and management networks.

The most important part of the lab was the failure simulation. After the LEAF-01 to SPINE-01 uplink was intentionally disabled, OSPF detected the topology change and automatically redirected traffic through SPINE-02. End-to-end connectivity remained available throughout the failure.

After the failed link was restored, OSPF reconverged and both redundant paths returned to service.

This lab provided hands-on experience with the type of cabling, interface configuration, verification, fault isolation, redundancy, and network troubleshooting used in data center environments.
