Project 01: Virtual Network Lab Setup and Connectivity Validation

Objective

Build and validate an isolated virtual network lab to understand IP addressing, network interfaces, routing, ARP, and connectivity troubleshooting.

Lab Environment

- Virtualization: Oracle VirtualBox
- Attacker/Test Machine: Parrot OS
- Target Machine: Metasploitable 2
- Client Machine: Windows

Network Configuration

Device| IP Address
Parrot OS| 192.168.56.103/24
Windows Host-Only| 192.168.56.104/24
Metasploitable 2| 192.168.56.102

Practical Tasks Completed

- Verified connectivity between Windows and Parrot OS.
- Verified connectivity between Windows and Metasploitable 2.
- Confirmed Parrot OS connectivity to Metasploitable 2 with 0% packet loss.
- Inspected Parrot OS network interfaces using "ip -br addr".
- Inspected the routing table using "ip route".
- Inspected neighbor entries using "ip neigh".
- Identified the role of IP addresses, subnets, MAC addresses, and ARP.

Key Findings

- Devices on the same IPv4 subnet can communicate directly at Layer 2 without routing through a gateway, assuming the network and security settings permit it.
- ARP maps local IPv4 addresses to MAC addresses.
- The routing table identifies the interface used to reach a destination.
- A "STALE" neighbor entry does not necessarily indicate a connectivity failure.
- Successful ping tests confirm ICMP reachability, not that every service or port is accessible.

Troubleshooting Approach

When connectivity fails:

1. Verify the destination IP address.
2. Check the network adapter and interface status.
3. Confirm IP addresses and subnet masks.
4. Inspect the routing table.
5. Check firewall rules and repeat the connectivity test.

Security Relevance

Isolated virtual labs provide a controlled environment for practicing network configuration, connectivity validation, and troubleshooting before working with production networks.

Result

Successfully validated connectivity among the three lab machines and inspected network interfaces, routing information, and neighbor entries.

Tools Used

- Oracle VirtualBox
- Windows Command Prompt
- Parrot OS terminal
- ICMP ping
- Linux networking commands
