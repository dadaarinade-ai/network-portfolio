# Wireshark Mastery for Junior Network Security Analysts

This project demonstrates my practical mastery of **Wireshark**, a leading network protocol analyzer, as a Junior Network Security Analyst. 

I captured, analyzed, and interpreted network traffic from my own device to learn:

- TCP and UDP communication
- DNS analysis
- TCP flags (SYN, ACK, FIN, RST)
- QUIC and TLS traffic analysis
- Application identification using ports and SNI
- Detection of normal vs suspicious network behavior

---

## Project Structure

- **Captures/**: Contains sample Wireshark `.pcap` files  
- **Analysis-Reports/**: Step-by-step analysis of the captures  
- **Cheatsheet.md**: Quick reference for Wireshark filters and commands

---

## Key Skills Demonstrated

1. **Traffic Capture & Protocol Hierarchy**  
   Identified the percentage of traffic per protocol, including TCP, UDP, QUIC, DNS, TLS.

2. **Conversations**  
   Analyzed top talkers between my device and external IPs (Google, MTN servers).

3. **TCP Flags**  
   Understood the 3-way handshake and connection termination (SYN, ACK, FIN, RST).

4. **DNS Analysis**  
   Filtered DNS traffic, identified normal vs suspicious domains, and highlighted repeated queries.

5. **QUIC & TLS Analysis**  
   Identified encrypted traffic and used Server Name Indication (SNI) to map traffic to apps (YouTube, Google Ads).

6. **Application Identification**  
   Mapped traffic to apps using ports, protocols, and SNI.

7. **Security Insights**  
   Detected normal SYN patterns and understood how to recognize abnormal scans.

---

## Example Findings

- Top talkers:
  - `10.0.2.15 → 197.210.176.236` (MTN server)  
  - `10.0.2.15 → 173.194.23.8` (Google services)  
- DNS Analysis:
  - `www.youtube.com` → YouTube app
  - `googleads.g.doubleclick.net` → Google Ads
  - `i1.ytimg.com` → YouTube video segments
- QUIC Traffic:
  - Destination IP `197.210.176.236` → MTN network handling QUIC traffic
- TCP Flags:
  - SYN, ACK, FIN, RST interpreted to monitor connection health

---

## Cheatsheet

Refer to `Cheatsheet.md` for all Wireshark filters, TCP flags explanation, and quick analysis commands.

---

This project demonstrates readiness to work in **SOC/Network Security Analyst roles** by analyzing real network traffic.

