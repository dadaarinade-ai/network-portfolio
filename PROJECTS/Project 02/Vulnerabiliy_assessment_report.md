Vulnerability Assessment Report

|Project 02 — Network Reconnaissance and Vulnerability Assessment|
|--|
|Assessment Target: Metasploitable2|
|Target IP: "192.168.56.102"|
|Assessment Tool: Nmap 7.93|
|Assessment Date: 2 November 2026|
|Environment: Isolated VirtualBox Lab|
|Assessment Type: Network-Based Vulnerability Assessment|
|Assessor: Arinade Dada|

---

1. Executive Summary

A network-based vulnerability assessment was conducted against a Metasploitable2 virtual machine using Nmap's vulnerability detection scripts.

The assessment identified multiple potential security weaknesses, including a backdoor vulnerability associated with vsFTPd 2.3.4, an UnrealIRCd backdoor indicator, weaknesses in SSL configurations, and potential denial-of-service exposure.

The most significant finding was the vsFTPd 2.3.4 backdoor associated with CVE-2011-2523. Nmap reported this finding as exploitable, with scan evidence indicating root-level command execution.

These findings demonstrate how vulnerable services, outdated software, and insecure configurations can increase a system's attack surface.

Remediation and further validation are recommended.

2. Assessment Scope

2.1 Target Information

|Parameter| Details|
|--|--|
|Target| Metasploitable2|
|IP Address| 192.168.56.102|
|Operating System| Linux 2.6.x (Nmap estimate)|
|Network| 192.168.56.0/24|
|Scanner| Parrot OS|
|Scanner IP| 192.168.56.103|
|Assessment Tool| Nmap 7.93|

2.2 Assessment Boundaries

The assessment was restricted to the Metasploitable2 virtual machine within an isolated VirtualBox laboratory network.

The assessment focused on:

- Identifying potential vulnerabilities.
- Reviewing exposed services.
- Examining known service-related security weaknesses.
- Evaluating potential security impacts.
- Recommending remediation measures.

No external systems were included in the assessment.

3. Assessment Methodology

The following Nmap command was used:

sudo nmap --script vuln 192.168.56.102

The command executes Nmap vulnerability detection scripts against the specified target.

Scan duration: Approximately 327.94 seconds.

The scan output was reviewed to identify vulnerability indicators, affected services, and supporting evidence.

4. Detailed Vulnerability Findings

Finding 1: vsFTPd 2.3.4 Backdoor

Affected Port: 21/TCP
Service: FTP
Detected Version: vsFTPd 2.3.4
Associated CVE: CVE-2011-2523
Nmap Result: VULNERABLE (Exploitable)
Suggested Severity: Critical

Description

Nmap identified a backdoor vulnerability associated with vsFTPd version 2.3.4.

The vulnerability is associated with a compromised distribution of the software that can allow an attacker to obtain unauthorized command execution.

Evidence

The Nmap scan returned:

uid=0(root) gid=0(root)

This indicates that the command executed by the detection script returned root-level privileges.

Potential Impact

- Unauthorized remote command execution.
- Privileged access to the target system.
- Potential compromise of system confidentiality, integrity, and availability.

Recommended Remediation

- Remove the vulnerable software version.
- Install a trusted, supported FTP service version if FTP is required.
- Prefer secure file-transfer alternatives such as SFTP.
- Restrict access to file-transfer services using firewall rules.
- Review system logs for suspicious activity.

Validation

Repeat service detection and vulnerability checks after remediation to confirm that the vulnerable version and backdoor exposure are no longer present.

---

Finding 2: UnrealIRCd Backdoor Indicator

Affected Port: 6667/TCP
Service: IRC
Nmap Result: Backdoor indicator reported
Suggested Severity: High

Description

The assessment identified a backdoor indicator associated with the UnrealIRCd service.

A backdoor in an IRC service can potentially allow unauthorized users to execute commands on the affected system.

Potential Impact

- Unauthorized remote access.
- Remote command execution.
- Potential compromise of the target machine.

Recommended Remediation

- Verify the installed UnrealIRCd version and software integrity.
- Remove or replace compromised software.
- Disable the IRC service if it is not required.
- Restrict access to the service through firewall rules.

Validation

Repeat service detection and the relevant vulnerability checks after remediation.

---

Finding 3: SSL POODLE and Weak Diffie-Hellman Configuration

Affected Ports:

- 25/TCP — SMTP
- 5432/TCP — PostgreSQL

Nmap Findings: SSL POODLE and weak Diffie-Hellman indicators
Suggested Severity: Medium to High, pending configuration validation

Description

Nmap reported SSL POODLE and weak Diffie-Hellman configuration findings on the identified services.

POODLE is associated with weaknesses in SSL 3.0. Weak Diffie-Hellman configurations can reduce the security of encrypted connections.

Potential Impact

- Reduced confidentiality of encrypted communications.
- Increased exposure to cryptographic attacks.
- Potential compromise of sensitive information under vulnerable conditions.

Recommended Remediation

- Disable SSL 3.0 and other obsolete protocols.
- Configure supported TLS versions.
- Use strong Diffie-Hellman parameters and secure cipher suites.
- Review the cryptographic configurations of SMTP and PostgreSQL.

Validation

Use appropriate SSL/TLS assessment tools and repeat the relevant Nmap checks to verify the configurations.

---

Finding 4: OpenSSL CCS Injection

Affected Port: 5432/TCP
Service: PostgreSQL
Nmap Finding: OpenSSL CCS Injection
Suggested Severity: High, pending validation

Description

Nmap reported an OpenSSL ChangeCipherSpec (CCS) Injection vulnerability indicator on the PostgreSQL service.

This vulnerability is associated with certain vulnerable OpenSSL implementations and can affect the security of encrypted connections.

Potential Impact

- Potential compromise of encrypted communications.
- Reduced security of TLS sessions.
- Exposure of sensitive information under affected conditions.

Recommended Remediation

- Identify the installed OpenSSL version.
- Upgrade affected OpenSSL components to a supported, patched version.
- Review PostgreSQL TLS configuration.
- Restart affected services after applying security updates.

Validation

Verify the installed OpenSSL version and repeat the relevant vulnerability checks.

---

Finding 5: Slowloris Denial-of-Service Exposure

Affected Port: 80/TCP
Service: HTTP
Nmap Finding: Slowloris exposure
Suggested Severity: Medium

Description

The Nmap scan reported potential exposure to Slowloris, an application-layer denial-of-service technique.

Slowloris attempts to exhaust web-server connection resources by maintaining incomplete HTTP requests.

Potential Impact

- Exhaustion of available server connections.
- Reduced web-server performance.
- Denial of service to legitimate users.

Recommended Remediation

- Apply appropriate web-server updates.
- Configure connection and request timeouts.
- Implement connection limits.
- Use suitable reverse-proxy or web application protection controls.

Validation

Review the web-server configuration and conduct authorised testing to verify its resilience.

---

Finding 6: Exposed Java RMI Registry

Affected Port: 1099/TCP
Service: Java RMI Registry
Nmap Finding: Exposed service identified
Suggested Severity: Requires further assessment

Description

The scan identified a Java RMI registry accessible on port 1099.

Remote Method Invocation allows Java applications to communicate with remote objects. An exposed or poorly configured RMI registry can increase the attack surface.

Potential Impact

- Unauthorized interaction with remote services.
- Exposure of application functionality.
- Potential remote exploitation depending on configuration and implementation.

Recommended Remediation

- Disable the RMI service if it is unnecessary.
- Restrict access to trusted hosts.
- Apply appropriate authentication and security controls.
- Review the application's RMI configuration.

Validation

Review the service configuration and perform further authorised security testing.

---

5. Risk Prioritisation

The following table provides preliminary remediation priorities based on the potential impact of the reported findings.

|Finding| Preliminary Priority|
|--|--|
|vsFTPd backdoor| Critical|
|UnrealIRCd backdoor indicator| High|
|OpenSSL CCS Injection| High|
|SSL POODLE and weak Diffie-Hellman| Medium–High|
|Slowloris exposure| Medium|
|Java RMI exposure| Further assessment required|

Risk assessment note: These are preliminary qualitative priorities, not formally calculated CVSS scores. Final severity should consider exploitability, exposure, asset importance, and validated technical evidence.

6. Remediation and Verification Plan

|Finding| Recommended Action| Verification|
|--|--|--|
|vsFTPd backdoor| Replace vulnerable software| Repeat version and vulnerability scans|
|UnrealIRCd backdoor| Verify integrity and replace affected software| Repeat service and vulnerability checks|
|SSL weaknesses| Strengthen TLS configuration| Repeat SSL/TLS assessment|
|OpenSSL CCS Injection| Patch affected OpenSSL components| Verify version and rerun checks|
|Slowloris| Apply web-server protections| Review configuration and test resilience|
|Java RMI| Restrict or disable unnecessary access| Review configuration and access controls|

7. Assessment Limitations

The following limitations apply:

1. Nmap vulnerability scripts provide automated detection and do not independently prove every vulnerability.
2. Some findings require manual validation.
3. An exposed service does not automatically mean that the service is exploitable.
4. The assessment did not include a complete manual penetration test.
5. The findings are limited to the target and configuration observed during the assessment.

8. Conclusion

The vulnerability assessment identified multiple security weaknesses within the Metasploitable2 environment.

The vsFTPd 2.3.4 backdoor was the most significant scan-reported finding because of its potential to provide remote command execution with root-level privileges.

Other findings highlighted weaknesses in encrypted communication, potentially vulnerable network services, and unnecessary exposure.

The assessment demonstrates the importance of regular vulnerability scanning, service management, secure configuration, and timely software updates.

9. Evidence References

Supporting screenshots and scan outputs are maintained in the project's "screenshots" directory.

Recommended evidence:

- Host discovery results.
- Open TCP port scan.
- Service and version detection.
- Operating system detection.
- Vulnerability scan output.

The original vulnerability scan output should also be retained as supporting evidence.

10. Authorization Statement

This assessment was conducted on an intentionally vulnerable Metasploitable2 virtual machine within a personally configured, isolated VirtualBox laboratory environment.

The work was performed for educational and professional development purposes.
