# Nmap Basic Scan — Windows host (Day 3 / Day 4)

## Summary
Performed Nmap scans from a Windows host against local network devices discovered on 10.81.119.0/24.  
Targets: 10.81.119.126 (host) and gateway 10.81.119.166. Goal: enumerate live hosts, identify open services and versions, and recommend mitigations.

## Environment
- Host OS: Windows 11 (PowerShell).  
- Tool versions: Nmap 7.98, Git 2.51.0.windows.1, PowerShell 5.1.22621.963.
- Dates: 2025-10-25 (scan timestamps saved in nmap/* files).
- Files (raw): see Appendix.

## Method
1. Host discovery: `nmap -sn 10.81.119.0/24` → `nmap/nmap_ping_scan.txt`.
2. Quick port enumeration (top-1000): `nmap -Pn --top-ports 1000 -oG quick_<ip>_grep.txt`.
3. Targeted service detection on discovered open ports: `nmap -Pn -sV -sC -p <ports> -oN targeted_<ip>_services.txt`.

## Findings

### Host: 10.81.119.126
- **135/tcp — open — msrpc**  
  Evidence (from `nmap/targeted_10.81.119.126_services.txt`): `135/tcp open msrpc Microsoft Windows RPC`
- **139/tcp — open — netbios-ssn**  
  Evidence: `139/tcp open netbios-ssn Microsoft Windows netbios-ssn`
- **445/tcp — open — microsoft-ds (SMB)**  
  Evidence: `445/tcp open microsoft-ds?`  
  Host script notes: SMB2 message signing **enabled but not required** (NSE output: `smb2-security-mode: Message signing enabled but not required`), which is a potential configuration weakness.

Service info: OS: Windows; CPE: `cpe:/o:microsoft:windows`

---

### Host: 10.81.119.166
- **53/tcp — open — domain (DNS, dnsmasq 2.51)**  
  Evidence (from `nmap/targeted_10.81.119.166_services.txt`): `53/tcp open domain dnsmasq 2.51`  
  NSE output shows `id.server: internet` and `bind.version: dnsmasq-2.51`.

---

## Risk & Recommendation

### 445/tcp (SMB – microsoft-ds)
- **Risk:** SMB exposure may allow unauthorized file access, credential theft, and lateral movement. If SMB is reachable from untrusted networks it's high risk.
- **Recommendations:**
  1. Disable SMBv1: `Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol`.
  2. Restrict SMB (TCP 445) via firewall to only trusted IPs; block at perimeter from the Internet.
  3. Enforce SMB signing and ensure strong authentication; apply Windows updates.

### 135/tcp (MSRPC) & 139/tcp (NetBIOS-SSN)
- **Risk:** Legacy services can leak host info and be abused for reconnaissance/exploitation.
- **Recommendations:**
  - Disable NetBIOS over TCP/IP if not required.
  - Harden host firewall rules to limit RPC/NetBIOS exposure.
  - Keep OS patched and audit RPC-related activity.

### 53/tcp (DNS — dnsmasq 2.51)
- **Risk:** Outdated dnsmasq may contain known vulnerabilities; exposed recursive DNS can be abused for amplification.
- **Recommendations:**
  - Update dnsmasq to the latest stable release.
  - Restrict recursion to internal clients and bind DNS only to intended interfaces.
  - Monitor DNS logs for unusual query patterns.

---

## Detection Notes
- SMB/NetBIOS: look for unexpected connections to dst_port 445/139; alert on many failed authentication events (EventID 4625) and new service or process creation following network access.
- DNS: alert on high query rates, high NXDOMAIN rates, and large payloads indicative of amplification.
- Port scans: alert when a single src_ip probes many dst_ports in a short window.

---

## Appendix (raw outputs included)
Place these files in `C:\network-portfolio\nmap` and commit to repo:

- nmap/nmap_ping_scan.txt
- nmap/quick_10.81.119.126_grep.txt
- nmap/quick_10.81.119.166_grep.txt
- nmap/targeted_10.81.119.126_services.txt
- nmap/targeted_10.81.119.126_services.xml
- nmap/targeted_10.81.119.166_services.txt
- nmap/targeted_10.81.119.166_services.xml

