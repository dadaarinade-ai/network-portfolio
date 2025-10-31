# 🧠 Day 7 – SIEM: Splunk Log Ingestion (Part 1)

**Objective:**  
Set up Splunk Enterprise to ingest external network scan logs (from Nmap) and verify that data is successfully indexed for analysis.

---

## 🔧 Steps Taken
1. Installed Splunk Enterprise locally.
2. Added file monitor input for:
   `C:\Users\user\network-portfolio\Projects-nmap-scan\sample2_log.txt`
3. Verified ingestion with:

and

4. Confirmed events appeared in the **main** index.

---

## 🧩 Results
- Splunk successfully indexed the log file.  
- Source visible via metadata search.  
- File monitoring active for new data.

---

## 🧠 Lessons Learned
- Splunk ingests structured/unstructured text logs.  
- Continuous monitoring ensures real-time SIEM data ingestion.

---

## 🚀 Next Step (Day 8)
Create dashboards to visualize top hosts, open ports, and write the short detection report.

**Status:** ✅ Day 7 complete  
**Next:** Day 8 – Splunk SIEM Dashboard & Report
