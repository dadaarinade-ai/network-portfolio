
# Project 03: Network Traffic Analysis and Suspicious Traffic Investigation Using Wireshark

## 1. Project Overview

This project focuses on analysing network traffic using Wireshark to understand communication protocols and identify suspicious network activities.

Practical exercises included analysing ICMP, TCP, HTTP, DNS and UDP traffic, as well as investigating TCP port scanning activity.

## 2. Lab Environment

|Component| Configuration|
|--|--|
|Host Machine| Windows|
|Virtualisation| Oracle VirtualBox|
|Attacker/Analysis Machine| Parrot OS|
|Target Machine| Metasploitable2|
|Wireshark Version| 4.0.4|
|Nmap Version| 7.93|
|Host-only Network| 192.168.56.0/24|
|Parrot OS IP| 192.168.56.103|
|Metasploitable2 IP| 192.168.56.102

## 3. Objectives

- Understand how network protocols communicate.
- Analyse ICMP, TCP, HTTP, DNS and UDP packets.
- Understand TCP three-way handshake and connection termination.
- Measure DNS response time.
- Identify suspicious network traffic.
- Recognise possible TCP port scanning activity.

## 4. Practical Exercises

#### Exercise 1: ICMP Traffic Analysis

Generated ICMP traffic between Parrot OS and Metasploitable2.

Observation:

- ICMP Echo Requests (Type 8).
- ICMP Echo Replies (Type 0).

Finding: Successful ICMP communication confirmed connectivity between the two virtual machines.

#### Exercise 2: TCP Handshake Analysis

Generated HTTP traffic using:

"curl http://192.168.56.102"

Observation:

- SYN
- SYN-ACK
- ACK
- FIN-ACK

Finding: Observed TCP connection establishment and termination.

#### Exercise 3: HTTP Traffic Analysis

Applied the HTTP display filter and inspected the TCP stream.

Observation:

"GET / HTTP/1.1"

Finding: HTTP requests can expose readable information because HTTP does not encrypt application data.

Security Finding:HTTP transmits application data without encryption. This means that requests and responses can be captured and read by anyone with access to the network traffic.

During this exercise, the HTTP GET request was visible in Wireshark, demonstrating how unencrypted web communication can expose information to network observers.

#### Exercise 4: DNS Traffic Analysis

Generated DNS queries using:

"nslookup example.com"

Observation:

- DNS Standard Query.
- DNS Standard Query Response.
- A and AAAA records.

DNS response time calculation:

Query timestamp: 42.955768652 seconds

Response timestamp: 42.956627248 seconds

Response time: approximately 0.859 milliseconds.

Finding: The DNS response was received in less than one millisecond in this capture.

#### Exercise 5: UDP Traffic Analysis

Inspected UDP traffic and DNS communication.

Observation:

- DNS server destination port: 53.
- Client source port: 48868.
- DNS query and response packets.

Finding: UDP does not require a TCP three-way handshake and does not provide built-in delivery or ordering guarantees.

#### Exercise 6: Suspicious Traffic Investigation — TCP Port Scanning

Generated a TCP SYN scan using:

"sudo nmap -sS -p 1-1000 192.168.56.102"

Applied Wireshark display filters:

SYN requests:

"tcp.flags.syn == 1 && tcp.flags.ack == 0"

SYN-ACK responses:

"tcp.flags.syn == 1 && tcp.flags.ack == 1"

RST responses:

"tcp.flags.reset == 1"

Observed network addresses:

- Source: 192.168.56.103 (Parrot OS)
- Destination: 192.168.56.102 (Metasploitable2)

Findings:

- SYN packets represented connection requests to different destination ports.
- SYN-ACK responses indicated ports accepting connection attempts.
- RST responses indicated closed ports.

The traffic pattern demonstrated TCP port scanning, a reconnaissance technique that can be used to identify exposed services.

## 5. Security Implications
##### Security Investigation and Recommended Response
A port scan is not automatically malicious. It may be performed during authorised vulnerability assessments, network troubleshooting or by an unauthorised individual conducting reconnaissance.

When suspicious scanning activity is detected, a Network Security Engineer should:
1. Identify the source and destination IP addresses.
2. Examine the destination ports and number of connection attempts.
3. Analyse the frequency and pattern of the scanning activity.
4. Verify whether the activity is authorised.
5. Document findings and escalate confirmed suspicious activity according to the organisation's incident response procedures.

Port scanning can help attackers identify:
- Open network ports.
- Running services.
- Potentially vulnerable services.
- Possible entry points into a network.

Network Security Engineers should investigate unusual scanning activity, identify the source and destination, verify whether the activity is authorised, and escalate suspicious findings according to incident response procedures.

Investigation Takeaway:
Network traffic analysis requires examining communication patterns, identifying unusual behaviour and gathering evidence before making security decisions

## 6. Evidence
6. Evidence

Screenshots

"View Wireshark Screenshots" (https://github.com/dadaarinade-ai/network-portfolio/tree/main/Wireshark-Mastery/Project%2003/Screenshots)

Packet Captures

"View Wireshark Packet Captures" (https://github.com/dadaarinade-ai/network-portfolio/tree/main/Wireshark-Mastery/Project%2003/Wireshark_capture_evidence)


Evidence includes:

- ICMP packet capture.
- TCP handshake capture.
- HTTP request capture.
- DNS query and response capture.
- UDP traffic capture.
- TCP SYN scan requests.
- SYN-ACK responses.
- RST responses.
- Original Wireshark packet capture files.

## 7. Conclusion

This practical exercise improved my understanding of network protocols and packet-level traffic analysis.

I gained hands-on experience using Wireshark to inspect network communication, measure DNS response time and investigate TCP port scanning activity.

The project demonstrates foundational network monitoring, traffic analysis and security investigation skills.
