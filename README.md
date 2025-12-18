Project Overview

This repository contains a Cisco Packet Tracer–based enterprise network simulation that demonstrates the integration of Inter-VLAN Routing, OSPF dynamic routing, and network security using Extended Access Control Lists (ACLs).

The topology represents a multi-department enterprise environment where each department is mapped to a distinct VLAN (color-coded). Although OSPF enables full routing visibility between routers, Extended ACLs enforce strict communication policies, ensuring that only identical VLANs (same color) are permitted to communicate across the routed infrastructure, while all inter-VLAN traffic is explicitly denied.

This project emphasizes network segmentation, scalability, and security using industry-standard Cisco technologies.

Key Features

Multi-VLAN architecture with logical segmentation

Inter-VLAN routing using Router-on-a-Stick (802.1Q)

Dynamic routing with OSPF (Area 0)

VLAN-level isolation using Extended ACLs

Enterprise-style addressing and structured design

Fully functional and testable in Cisco Packet Tracer

Technical Specifications

Routing Protocol: OSPF (Open Shortest Path First), Area 0

Inter-VLAN Routing: Router-on-a-Stick (IEEE 802.1Q)

Security Mechanism: Extended Access Control Lists (ACLs)

VLAN IDs:

VLAN 10 – Red

VLAN 20 – Blue

VLAN 30 – Yellow

VLAN 40 – Green

Network Devices:

Cisco 2911 Routers

Cisco 2960 Switches

Host Identification: All PC IP addresses reflect Roll Number 63

Network Architecture & IP Addressing
VLAN-Based Subnet Allocation
VLAN Color	VLAN ID	Router 0 Subnet	Router 1 Subnet
Red	10	192.168.10.0/24	192.168.11.0/24
Blue	20	192.168.20.0/24	192.168.21.0/24
Yellow	30	192.168.30.0/24	192.168.31.0/24
Green	40	192.168.40.0/24	192.168.41.0/24

Serial Link Between Routers:

Network: 10.10.10.0/30

Router 0: 10.10.10.1

Router 1: 10.10.10.2

PC IP Configuration (Roll Number–Based)
PC Name	VLAN Color	IP Address	Default Gateway
PC0	Red	192.168.10.63	192.168.10.1
PC8	Red	192.168.11.63	192.168.11.1
PC2	Blue	192.168.20.63	192.168.20.1
PC10	Blue	192.168.21.63	192.168.21.1

(Complete host list and interface configurations are available inside the Packet Tracer file.)

Configuration Highlights
1. VLAN Trunking Configuration (Switches)

Trunk links are configured on the distribution switches to carry tagged VLAN traffic to the routers.

enable
configure terminal
interface range fa0/1 - 3
 switchport mode trunk

2. OSPF Configuration (Router 0 Example)
router ospf 1
 network 10.10.10.0 0.0.0.3 area 0
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 0

3. Extended ACL-Based VLAN Isolation

Extended ACLs are applied to router sub-interfaces to allow same-VLAN communication across routers while blocking all inter-VLAN traffic.

Example: Red VLAN (Router 0)

access-list 110 permit ip 192.168.10.0 0.0.0.255 192.168.11.0 0.0.0.255
access-list 110 permit ip 192.168.10.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 110 deny   ip 192.168.10.0 0.0.0.255 192.168.0.0 0.0.255.255


This approach ensures strict departmental isolation while preserving required connectivity.

How to Run the Lab

Download the .pkt file from this repository.

Open the file using Cisco Packet Tracer v8.0 or later.

Allow time for OSPF convergence (verify active serial links).

Test connectivity:

Ping PC0 (Red) → PC8 (Red) → ✅ Successful

Ping PC0 (Red) → PC2 (Blue) → ❌ Blocked (ACL enforced)

Author

Roll Number:SP24-BCS-063
Program: BS Computer Science
Semester: 4

Note

This project was developed solely for educational purposes to demonstrate the interaction between dynamic routing protocols and network security mechanisms in a segmented, multi-tenant enterprise environment.
