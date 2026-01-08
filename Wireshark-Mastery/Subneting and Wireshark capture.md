Subnetting Practice + Wireshark Capture

Project Title: Network Traffic Capture and Analysis

Objective:
To understand basic subnetting, capture live network traffic, and analyze key packet details using Wireshark.

---
Subnetting Practice:
- Reviewed subnetting concepts: IP address, subnet mask, network ID, broadcast address.
- Practiced dividing a /24 network into smaller subnets (/26, /28).
- Learned how subnetting improves IP allocation and security segmentation.

Example:
Network: 192.168.1.0/24
Subnet Mask: 255.255.255.0
Subnets Created: 4 (each /26)
Usable IPs per subnet: 62

---
 Wireshark Traffic Capture:
Steps performed:
1. Opened Wireshark and selected Wi-Fi interface.
2. Captured packets while browsing google.com and opening YouTube.
3. Stopped capture after 30 seconds.
4. Analyzed protocols seen in packets (DNS, TCP, HTTPS, ARP).

Example Observation:
- DNS request for www.google.com
- TCP 3-way handshake between client and server
- HTTPS encrypted packets showing secure data exchange

---
 Commands Used:
- ipconfig /all — To check current IP configuration
- ping 8.8.8.8 — To verify Internet connectivity
- Wireshark — To view live network packets
- netstat -ano — To see open connections and ports

---
 Summary:
• Understood subnetting logic and IP division.
• Captured real network traffic using Wireshark.
• Observed DNS resolution and TCP connections.
• Learned to identify normal vs suspicious traffic.

