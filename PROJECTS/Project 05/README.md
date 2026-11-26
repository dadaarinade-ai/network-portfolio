# Project 05: VLAN Configuration and Inter-VLAN Routing

### 1. Project Overview

This project demonstrates how to segment a company network into separate Virtual Local Area Networks (VLANs) and enable communication between departments using Inter-VLAN Routing.

The project also implements an Extended Access Control List (ACL) to restrict communication from the Sales department to the Administration department.

### 2. Project Objectives

- Create VLANs for Administration, IT, and Sales.
- Assign switch ports to the appropriate VLANs.
- Configure an IEEE 802.1Q trunk link.
- Implement Router-on-a-Stick for Inter-VLAN Routing.
- Configure an Extended ACL to enforce department-level access restrictions.
- Test network connectivity and verify ACL behaviour.

### 3. Network Topology

The network consists of:

- One Cisco 1841 router.
- One Ethernet switch.
- Three end devices representing company departments.

The router connects to the switch through a trunk link.

### 4. VLAN Configuration

|Department| VLAN ID| Assigned Switch Port|
|--|--|--|
|Administration| 10| Fa0/2|
|IT| 20| Fa0/3|
|Sales| 30| Fa0/4|

### 5. IP Addressing Scheme

|Department| Network| Gateway|
|--|--|--|
|Administration| 192.168.10.0/26| 192.168.10.1|
|IT| 192.168.10.64/26| 192.168.10.65|
|Sales| 192.168.10.128/26| 192.168.10.129|

### 6. Trunk Configuration

The switch port GigabitEthernet0/1 was configured as an 802.1Q trunk to carry traffic for the different VLANs between the switch and router.

### 7. Inter-VLAN Routing

Router-on-a-Stick was implemented using three router subinterfaces:

- Fa0/0.10 — Administration
- Fa0/0.20 — IT
- Fa0/0.30 — Sales

Each subinterface was configured with its respective VLAN encapsulation and default gateway address.

### 8. Access Control List (ACL)

An Extended ACL named "SALES-RESTRICTION" was configured and applied inbound on router subinterface Fa0/0.30.

Security Policy

- Block traffic initiated from Sales to Administration.
- Permit Sales-to-IT communication.
- Permit Sales traffic to other destinations.
- Allow ICMP echo-reply traffic from Sales to Administration.

Note: The ACL is stateless. The ICMP exception permits ping replies, but it does not provide general stateful session tracking.

### 9. Testing and Results

|Test| Expected Result| Observed Result|
|--|--|--|
|Administration to its gateway| Success| Successful|
|IT to its gateway| Success| Successful|
|Sales to its gateway| Success| Successful|
|Administration to IT| Success| Successful|
|Administration to Sales| Success| Successful|
|IT to Administration| Success| Successful|
|IT to Sales| Success| Successful|
|Sales to Administration| Blocked| Blocked|
|Sales to IT| Success| Successful|

The ACL hit counters also confirmed that the deny and permit rules were matching traffic.

### 10. Skills Demonstrated

- VLAN creation and configuration
- Switch port assignment
- 802.1Q trunking
- Router-on-a-Stick configuration
- Inter-VLAN Routing
- Extended Access Control Lists
- Network segmentation
- Connectivity testing and troubleshooting
- Network security policy enforcement

### 11. Project Evidence

Screenshots and the Cisco Packet Tracer simulation are available in the Evidence directory.

### 12. Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI

### 13. Conclusion

This project demonstrates how VLANs can be used to logically segment an enterprise network, how Inter-VLAN Routing enables controlled communication between departments, and how Extended ACLs can enforce basic network access restrictions.
