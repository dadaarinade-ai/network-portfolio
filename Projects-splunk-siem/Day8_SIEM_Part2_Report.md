# 📊 Day 8: SIEM – Splunk Dashboard (Part 2)

### 🎯 Objective
Finalize the Splunk dashboard to visualize Nmap scan data and summarize network visibility.

---

### ⚙️ Dashboard Panels Created
| Panel | Description | Visualization |
|--------|--------------|----------------|
| 🟩 **Total Unique Hosts** | Counts unique hosts detected from Nmap logs | Single Value |
| 🟦 **Open Ports per Host** | Displays number of open ports found on each host | Bar Chart |
| 🟪 **Top Services Detected** | Lists top services found across open ports | Pie Chart |

---

### 🧩 Key Queries Used

#### 🟩 Total Unique Hosts
```splunk
index=main "Nmap scan report for"
| rex "Nmap scan report for (?<host>[0-9\.]+)"
| stats dc(host) as "Unique Hosts Detected"
index=main "open"
| rex "^(?<port>\d+)/tcp\s+open\s+(?<service>\S+)"
| eval host="localhost"
| stats count(port) as "Open Ports" by host
| sort - "Open Ports"
index=main "open"
| rex "^(?<port>\d+)/tcp\s+open\s+(?<service>[\w\-/]+)"
| stats count by service
| sort -count
| head 10
📈 Dashboard Insights

Found 5 open ports on localhost

Common services: msrpc, microsoft-ds, http, ssl/http

Dashboards visualize network exposure effectively
💡 Key Learnings

Extracted and visualized log data using Splunk regex

Created custom SIEM dashboards                                                                                                                                              Turned raw Nmap logs into security insights                                                                                                                                 Author: Arinade Dada
Date: November 2025
Repository:  [Network Portfolio](https://github.com/dadaarinade-ai/network-portfolio)
