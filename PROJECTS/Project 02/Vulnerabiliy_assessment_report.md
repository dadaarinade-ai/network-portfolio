
Vulnerability Assessment Report

1. **Project Overview**

Project Title: Network Reconnaissance and Vulnerability Assessment Using Nmap
Target: Metasploitable2
Target IP Address: "192.168.56.102"
Operating System: Linux 2.6.x (Nmap OS estimate)
Tool Used: Nmap 7.93
Assessment Environment: Isolated VirtualBox network lab

2. **Objective**

The objective of this assessment was to identify potential security vulnerabilities and weaknesses in the Metasploitable2 virtual machine using Nmap's vulnerability detection scripts.

The assessment focused on identifying vulnerable services, outdated software, insecure configurations, and possible attack entry points.

3. **Methodology**

The following Nmap command was executed:

sudo nmap --script vuln 192.168.56.102

This command runs Nmap's vulnerability detection scripts against the target to identify known security weaknesses.

The scan took approximately 327.94 seconds to complete.

4. **Key Findings**

The scan reported the following security issues:

|Service / Port| Finding| Potential Risk|
|--|--|--|
|FTP - 21| vsFTPd 2.3.4 backdoor (CVE-2011-2523)| Remote command execution|
|IRC - 6667| UnrealIRCd backdoor indicator| Possible remote command execution|
|HTTP - 80| Slowloris exposure| Denial of Service|
|SMTP - 25| SSL POODLE and weak Diffie-Hellman| Weaknesses in encrypted communication|
|PostgreSQL - 5432| SSL POODLE, weak Diffie-Hellman and OpenSSL CCS Injection| Potential compromise of secure communication|
|Java RMI - 1099| Exposed Java RMI registry| Potential remote service abuse|

Note: These are scan-reported findings. They have not all been independently validated.

5. **Risk Analysis**

5.1 vsFTPd Backdoor — Port 21

Nmap reported that vsFTPd version 2.3.4 was vulnerable to the backdoor associated with CVE-2011-2523.

The scan output included evidence showing:

uid=0(root) gid=0(root)

This indicates that the command executed by the vulnerability detection script returned root-level privileges.

Potential impact: An attacker could gain unauthorized access and execute commands with elevated privileges.

5.2 UnrealIRCd Backdoor Indicator — Port 6667

The scan identified a backdoor indicator associated with the UnrealIRCd service.

Potential impact: An attacker could potentially execute commands remotely on the affected system.

Further validation is required to establish the exact exposure.

5.3 Slowloris — Port 80

The HTTP service was reported as potentially exposed to Slowloris denial-of-service attacks.

Potential impact: An attacker could exhaust available web-server connections, making the service unavailable to legitimate users.

5.4 SSL/TLS Weaknesses — Ports 25 and 5432

The scan reported SSL POODLE and weak Diffie-Hellman configurations on these services. It also reported OpenSSL CCS Injection on port 5432.

Potential impact: Weak cryptographic configurations may expose encrypted communications to attacks.

5.5 Java RMI Exposure — Port 1099

The Java RMI registry was accessible on port 1099.

Potential impact: An exposed or poorly secured RMI service may provide an attacker with an additional attack surface.

6. **Security Recommendations**

Based on the scan findings, the following security improvements are recommended:

1. Update vulnerable software: Replace outdated and vulnerable service versions with supported versions.
2. Disable unnecessary services: Stop services that are not required for business operations.
3. Secure FTP services: Replace insecure FTP configurations with secure file-transfer alternatives.
4. Strengthen SSL/TLS: Disable vulnerable protocols and weak cryptographic configurations.
5. Protect web services: Apply appropriate web-server configurations and denial-of-service protections.
6. Restrict service access: Use firewall rules and network segmentation to limit access to sensitive services.
7. Validate vulnerabilities: Conduct further testing to confirm scan-reported findings.

7. **Conclusion**

The Nmap vulnerability assessment identified multiple potential security weaknesses on the Metasploitable2 machine.

The most significant scan finding was the vsFTPd 2.3.4 backdoor associated with CVE-2011-2523, which was reported as exploitable by the Nmap script.

The assessment demonstrates how network reconnaissance and vulnerability scanning can help security engineers identify exposed services, outdated software, and potential attack vectors.

Regular vulnerability assessments, timely patching, secure service configurations, and network access controls are essential for reducing network security risks.

8. **Tools Used**

- Parrot OS
- Nmap 7.93
- Metasploitable2
- Oracle VirtualBox

9. **Project Scope and Authorization**

This assessment was conducted within a personally configured, isolated VirtualBox lab for educational and practical cybersecurity training.

No external systems were scanned or tested without authorization.
