# 🔐 SOC Incident Investigation: Brute Force Attack Detection (Splunk)

## 📌 Overview

This project simulates a real-world Security Operations Center (SOC) investigation into a potential brute-force login attack using Splunk SIEM.

The objective was to:

* Ingest and analyze Windows Security logs
* Perform alert triage on failed login activity (EventCode 4625)
* Investigate authentication patterns and identify suspicious behavior
* Correlate failed and successful login events
* Document findings and recommend response actions following SOC workflows
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

## 🧭 Investigation Process

### 1. Alert Triage
Initial review focused on identifying repeated failed login attempts using EventCode 4625.

### 2. Pattern Analysis
Multiple failed login attempts were observed targeting the same user account within a short timeframe, indicating potential brute-force behavior.

### 3. Log Correlation
Failed login events were correlated with successful login events (EventCode 4624) to determine whether access was eventually gained.

### 4. Timeline Creation
Login activity was analyzed chronologically to understand the sequence of events and identify suspicious spikes in activity.

### 5. Conclusion
The activity matched known brute-force attack patterns and required escalation for further investigation.

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

![Failed Logins](https://github.com/dportersec/splunk-siem-brute-force-detection/blob/main/screenshots/failed_login_events_detailed.png)



---

### 🔹 Login Timeline (Failed → Successful)

![Login Timeline](https://github.com/dportersec/splunk-siem-brute-force-detection/blob/main/screenshots/login_activity_timeline.png)

---

### 🔹 Failed Login Count by User

![Stats Query](https://github.com/dportersec/splunk-siem-brute-force-detection/blob/main/screenshots/login_activity_timeline.png)

---

## 📈 Findings

* Detected a high volume of failed login attempts (EventCode 4625) within a short time window
* Identified repeated targeting of a single user account
* Observed a successful login (EventCode 4624) following multiple failures
* The pattern of activity is consistent with a brute-force login attempt
* No additional evidence confirmed full account compromise, but the behavior warranted escalation

---

## ⏱️ Incident Timeline

| Time | Event |
|------|------|
| Initial | Multiple failed login attempts detected (EventCode 4625) |
| Shortly after | Repeated attempts against same account observed |
| Later | Successful login recorded (EventCode 4624) |
| Final | Activity reviewed and flagged for escalation |

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

## ✅ Recommended Response Actions

* Escalate incident to senior analyst for further investigation
* Reset affected user credentials if compromise is suspected
* Implement account lockout policies after repeated failures
* Enable Multi-Factor Authentication (MFA)
* Monitor authentication logs for continued suspicious activity
* Investigate source systems generating failed login attempts

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

## 🛡️ SOC Relevance

This project demonstrates core Tier 1 SOC analyst responsibilities, including alert triage, log analysis, identifying suspicious authentication patterns, correlating events, documenting findings, and recommending escalation steps. These are essential skills used in real-world security operations environments.
