Multi-VLAN OSPF Network with Extended ACL Isolation

Project Overview
This project is a Cisco Packet Tracer–based network simulation that demonstrates
Inter-VLAN Routing, dynamic routing using OSPF, and network security through
Extended Access Control Lists (ACLs).

The topology represents an enterprise environment where multiple departments are
segmented using VLANs. Although OSPF enables routing information exchange between
routers, Extended ACLs are implemented to ensure that only same-VLAN (same-color)
networks are allowed to communicate across routers, while inter-VLAN traffic is
strictly blocked.

Technical Specifications
Routing Protocol: OSPF (Open Shortest Path First), Area 0
Inter-VLAN Routing: Router-on-a-Stick (802.1Q Encapsulation)
Security Mechanism: Extended Access Control Lists (ACLs)
VLAN IDs:
- VLAN 10 (Red)
- VLAN 20 (Blue)
- VLAN 30 (Yellow)
- VLAN 40 (Green)
Network Devices:
- Cisco 2911 Routers
- Cisco 2960 Switches
Host Identification: All PC IP addresses are based on Roll Number 63

Network Architecture and IP Addressing

VLAN Subnet Allocation
VLAN 10 (Red)
- Router 0 Subnet: 192.168.10.0/24
- Router 1 Subnet: 192.168.11.0/24

VLAN 20 (Blue)
- Router 0 Subnet: 192.168.20.0/24
- Router 1 Subnet: 192.168.21.0/24

VLAN 30 (Yellow)
- Router 0 Subnet: 192.168.30.0/24
- Router 1 Subnet: 192.168.31.0/24

VLAN 40 (Green)
- Router 0 Subnet: 192.168.40.0/24
- Router 1 Subnet: 192.168.41.0/24

Serial Link Between Routers
Network: 10.10.10.0/30
- Router 0: 10.10.10.1
- Router 1: 10.10.10.2

PC IP Configuration (Roll Number 63)

PC0 (Red)
IP Address: 192.168.10.63
Default Gateway: 192.168.10.1

PC8 (Red)
IP Address: 192.168.11.63
Default Gateway: 192.168.11.1

PC2 (Blue)
IP Address: 192.168.20.63
Default Gateway: 192.168.20.1

PC10 (Blue)
IP Address: 192.168.21.63
Default Gateway: 192.168.21.1

Configuration Summary

VLAN Trunking Configuration (Switches)
enable
configure terminal
interface range fa0/1 - 3
 switchport mode trunk

OSPF Configuration Example (Router 0)
router ospf 1
 network 10.10.10.0 0.0.0.3 area 0
 network 192.168.10.0 0.0.0.255 area 0
 network 192.168.20.0 0.0.0.255 area 0
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 0

Extended ACL Example (Red VLAN)
access-list 110 permit ip 192.168.10.0 0.0.0.255 192.168.11.0 0.0.0.255
access-list 110 permit ip 192.168.10.0 0.0.0.255 192.168.10.0 0.0.0.255
access-list 110 deny ip 192.168.10.0 0.0.0.255 192.168.0.0 0.0.255.255

How to Run the Lab
1. Download the Packet Tracer (.pkt) file from this repository.
2. Open it using Cisco Packet Tracer version 8.0 or later.
3. Wait for OSPF convergence between routers.
4. Test connectivity:
   - Ping from Red PC to Red PC across routers: Successful
   - Ping from Red PC to Blue PC: Blocked by ACL

Author
Roll Number: SP24-BCS-063
Program: BS Computer Science
Semester: 4

Note
This project was created for educational purposes to demonstrate VLAN segmentation,
OSPF routing, and access control mechanisms in a multi-VLAN enterprise network.
