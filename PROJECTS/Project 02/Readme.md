Project 02: Network Reconnaissance and Vulnerability Assessment Using Nmap

1. Project Overview

This project demonstrates practical network reconnaissance, port scanning, service enumeration, operating system detection, and vulnerability assessment using Nmap.

The assessment was performed against a Metasploitable2 virtual machine in an isolated VirtualBox lab environment.

The objective was to identify active hosts, discover exposed network services, determine service versions, estimate the target operating system, and identify potential security weaknesses.

2. Objectives

- Discover active devices on the lab network.
- Identify open TCP ports.
- Detect running services and their versions.
- Estimate the target operating system.
- Identify potential vulnerabilities.
- Analyse security risks and recommend remediation measures.

3. Lab Environment

Component| Configuration
Attacker Machine| Parrot OS
Target Machine| Metasploitable2
Scanner| Nmap 7.93
Attacker IP| 192.168.56.103
Target IP| 192.168.56.102
Network| 192.168.56.0/24
Virtualisation| Oracle VirtualBox
Network Type| Host-only

4. Tools Used

- Parrot OS
- Nmap 7.93
- Metasploitable2
- Oracle VirtualBox

5. Methodology

The assessment was conducted in the following stages.

Stage 1: Host Discovery

Command:

sudo nmap -sn 192.168.56.0/24

Purpose: Identify active hosts within the lab subnet without performing a port scan.

Stage 2: Port Scanning

Command:

sudo nmap 192.168.56.102

Purpose: Identify open TCP ports on the target machine.

Result: 24 open TCP ports were identified.

Stage 3: Service and Version Detection

Command:

sudo nmap -sV 192.168.56.102

Purpose: Identify services running on open ports and determine their versions.

Examples of identified services included FTP, SSH, HTTP, SMTP, MySQL, PostgreSQL, Samba, and IRC.

Stage 4: Operating System Detection

Command:

sudo nmap -O 192.168.56.102

Purpose: Estimate the operating system running on the target.

Result: Nmap identified the target as a general-purpose Linux system, with a 2.6.x kernel estimate.

Stage 5: Vulnerability Assessment

Command:

sudo nmap --script vuln 192.168.56.102

Purpose: Run Nmap vulnerability detection scripts against the target.

The scan took approximately 327.94 seconds.

6. Key Findings

The vulnerability scan reported several potential security weaknesses:

|Service| Port| Finding|
|--|--|--|
|vsFTPd| 21| Backdoor associated with CVE-2011-2523|
|UnrealIRCd| 6667| Backdoor indicator|
|HTTP| 80| Slowloris exposure|
|SMTP| 25| SSL POODLE and weak Diffie-Hellman|
|PostgreSQL| 5432| SSL POODLE, weak Diffie-Hellman and OpenSSL CCS Injection|
|Java RMI| 1099| Exposed RMI registry|

These are scan-reported findings and require appropriate validation before being treated as confirmed vulnerabilities.

For detailed analysis, see "Vulnerability Assessment Report" (vulnerability-assessment-report.md).

7. Security Recommendations

Based on the assessment, the following security measures are recommended:

1. Update or remove vulnerable software.
2. Disable unnecessary network services.
3. Replace insecure FTP configurations with secure alternatives.
4. Strengthen SSL/TLS configurations.
5. Implement firewall rules to restrict unnecessary access.
6. Review exposed remote services.
7. Conduct follow-up vulnerability assessments to verify remediation.

8. Evidence and Screenshots

Screenshots documenting the assessment process are available below.

|Evidence| Screenshot|
|--|--|
|Host Discovery| "Screenshots/VUL1.png"|
|Open Ports| "Screenshots/VUL2.png"|
|Service Detection| "Screenshots/VUL3.png"|
|OS Detection| "Screenshots/VUL4.png"|
|Vulnerability Scan| "Screenshots/VUL5.png" "Screenshots/VUL6.png" "Screenshots/VUL7.png" "Screenshots/VUL8.png" "Screenshots/VUL9.png" "Screenshots/VUL10.png" "Screenshots/VUL11.png" "Screenshots/VUL12.png" "Screenshots/VUL13.png" "Screenshots/VUL14.png" "Screenshots/VUL15.png" "Screenshots/VUL16.png"|

9. Skills Demonstrated

- Network reconnaissance
- Host discovery
- TCP port scanning
- Service enumeration
- Operating system fingerprinting
- Vulnerability assessment
- Nmap scripting engine (NSE)
- Security risk identification
- Vulnerability documentation
- Security remediation recommendations

10. Key Learning Outcomes

Through this project, I gained practical experience in:

- Identifying active devices on a network.
- Understanding exposed ports and their associated services.
- Identifying outdated service versions.
- Using Nmap for network and vulnerability assessment.
- Interpreting scan results and recognising potential security risks.
- Documenting findings and recommending security improvements.

11. Scope and Authorization

This project was conducted in an isolated VirtualBox laboratory environment for educational and professional development purposes.

The assessment targeted only the intentionally vulnerable Metasploitable2 virtual machine.

No external systems were scanned without authorization.

---

Project Category: Network Security Engineering
Project Status: Completed
Author: Arinade Dada
