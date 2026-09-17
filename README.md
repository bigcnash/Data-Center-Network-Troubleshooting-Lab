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
