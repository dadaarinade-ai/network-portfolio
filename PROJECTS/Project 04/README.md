# Project 04: IP Addressing and Subnetting Design

## 1. Project Overview
This project demonstrates the design and allocation of IPv4 subnets for a company with three departments: Administration, IT, and Sales. The goal was to create an organized IP addressing scheme that supports current devices and allows for future expansion.

## 2. Project Objectives
- Design an IPv4 addressing scheme using CIDR.
- Divide a /24 network into smaller subnets.
- Calculate network addresses, usable host ranges, and broadcast addresses.
- Allocate IP addresses and default gateways to departments.
- Validate connectivity between a PC and its configured router gateway.

## 3. Network Requirements
Each department requires 30 computer addresses, 2 printer addresses, and 1 gateway address, making 33 addresses per department.

## 4. Addressing Plan
Base network: 192.168.10.0/24

Subnet mask: 255.255.255.192 (/26)

Each /26 subnet provides 62 usable host addresses.

| Department | Network/CIDR | Gateway | Usable Range | Broadcast |
|---|---|---|---|---|
| Administration | 192.168.10.0/26 | 192.168.10.1 | 192.168.10.1–192.168.10.62 | 192.168.10.63 |
| IT | 192.168.10.64/26 | 192.168.10.65 | 192.168.10.65–192.168.10.126 | 192.168.10.127 |
| Sales | 192.168.10.128/26 | 192.168.10.129 | 192.168.10.129–192.168.10.190 | 192.168.10.191 |
| Reserved | 192.168.10.192/26 | N/A | 192.168.10.193–192.168.10.254 | 192.168.10.255 |

## 5. Packet Tracer Implementation
The network was modeled in Cisco Packet Tracer using a Cisco 1841 router, an Ethernet switch, and three PCs.

Configured PC addresses:
- ADMIN-PC: 192.168.10.10/26
- IT-PC: 192.168.10.70/26
- SALES-PC: 192.168.10.140/26

The Administration router gateway (192.168.10.1/26) was configured and successfully tested. IT (192.168.10.65) and Sales (192.168.10.129) gateways are planned addresses and have not yet been configured on the router.

## 6. Connectivity Testing
| Test | Result | Observation |
|---|---|---|
| ADMIN-PC to 192.168.10.1 | Pass | 4 packets received, 0% loss |
| IT-PC to its own IP | Pass | 4 packets received, 0% loss |
| IT-PC to SALES-PC | Fail as expected | Inter-subnet routing is not configured |

## 7. Key Lessons Learned
- How to divide a /24 network into /26 subnets.
- How to calculate network, broadcast, and usable host addresses.
- How to allocate gateways and endpoint addresses.
- Why devices in different IP subnets require a Layer 3 routing function to communicate.

## 8. Future Improvements
- Configure department VLANs and trunk links.
- Implement inter-VLAN routing.
- Apply access control policies between departments.

These improvements are planned for Project 05.

## 9. Project Files
- IP_Address_Allocation_Table.md
- Network_Topology.mmd
- Project_04_IP_Addressing_and_Subnetting.pkt
- Screenshots/
- 

## 10. Evidence and Screenshots

### Network Topology
-[Network Topology](PROJECTS/Project 04/Evidence/Screenshots/project_04 topology.png)

### IP Configuration
- [Administration PC](Screenshots/02_ADMIN_IP_Configuration.png)
- [IT PC](Screenshots/03_IT_IP_Configuration.png)
- [Sales PC](Screenshots/04_SALES_IP_Configuration.png)

### Connectivity Testing
- [Successful Administration Gateway Ping](Screenshots/05_Gateway_Ping_Test.png)
- [Inter-Subnet Connectivity Test](Screenshots/06_Inter_Subnet_Ping_Test.png)
