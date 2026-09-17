# Data-Center-Network-Troubleshooting-Lab
Cisco Packet Tracer data center lab featuring spine-leaf architecture, VLAN segmentation, OSPF dynamic routing, redundant paths, failure simulation, troubleshooting, and automatic failover.
# Data Center Network Redundancy & Troubleshooting Lab

## Project Overview

This project simulates a highly available data center network using Cisco Packet Tracer.

The environment was designed around a spine-leaf architecture with redundant network paths, segmented server networks, Layer 3 routing, and OSPF dynamic routing.

Rather than stopping after building a working topology, the lab included a simulated uplink failure to test how the network would respond. After the primary path was disabled, OSPF automatically rerouted traffic through the redundant spine switch while maintaining connectivity between the web and application servers.

The failed link was then restored and the network reconverged back to a healthy redundant state.

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
