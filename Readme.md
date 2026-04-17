# 🔐 SIEM Log Analysis: Brute Force Detection (Splunk)

## 📌 Overview

This project demonstrates a real-world Security Operations Center (SOC) workflow using Splunk SIEM to detect and analyze brute force login attempts on a Windows system.

The objective was to:

* Ingest Windows Security logs into Splunk
* Identify failed login attempts (EventCode 4625)
* Correlate login activity to detect suspicious behavior
* Document findings using industry-standard practices

---

## 🛠️ Tools & Technologies

* Splunk Enterprise (Free License)
* Windows Event Logs (Security.evtx)
* Local Windows Machine (Log Generation)

---

## 🔍 Detection Scenario: Brute Force Attack

A brute force attack was simulated by intentionally entering incorrect login credentials multiple times.

### Key Indicators:

* Multiple failed login attempts (EventCode 4625)
* Attempts occurred within seconds
* Same account targeted repeatedly
* Successful login (EventCode 4624) followed failures

---

## 📊 Splunk Queries Used

### 🔹 Failed Login Detection

```spl
index=main EventCode=4625
```

### 🔹 Failed Login Count by User

```spl
index=main EventCode=4625
| stats count by Account_Name, host
| sort -count
```

### 🔹 Login Timeline (Success + Failure)

```spl
index=main (EventCode=4624 OR EventCode=4625)
| table _time, EventCode, Account_Name, host
| sort -_time
```

---

## 📸 Screenshots

### 🔹 Failed Login Attempts (EventCode 4625)

![Failed Logins](screenshots/failed_logins_4625.png)



---

### 🔹 Login Timeline (Failed → Successful)

![Login Timeline](screenshots/login_timeline.png)

---

### 🔹 Failed Login Count by User

![Stats Query](screenshots/stats_query.png)

---

## 📈 Findings

* Detected multiple failed login attempts within a short time window
* Identified repeated targeting of a single user account
* Observed successful authentication following failed attempts
* Behavior aligns with brute force attack techniques

---

## 🧠 MITRE ATT&CK Mapping

* **T1110 – Brute Force**

---

## ⚠️ Security Impact

This type of activity may indicate:

* Credential guessing attacks
* Automated login attempts
* Potential unauthorized access if successful

---

## ✅ Recommendations

* Implement account lockout policies after repeated failures
* Enable Multi-Factor Authentication (MFA)
* Monitor login patterns using SIEM alerts
* Investigate unusual login times or sources

---

## 🚀 Skills Demonstrated

* SIEM log analysis using Splunk
* Windows Event Log investigation
* Threat detection and analysis
* MITRE ATT&CK framework mapping
* Security incident documentation

---

## 📁 Project Structure

```
siem-brute-force-detection/
│
├── README.md
├── screenshots/
├── queries/
└── report/
```

---

## 📌 Summary

This project simulates real SOC analyst responsibilities by detecting and analyzing a brute force attack using Splunk. It demonstrates practical experience in log analysis, threat detection, and incident reporting — key skills required for entry-level cybersecurity roles.
