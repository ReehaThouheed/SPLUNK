# 🔐 Windows Security Monitoring Dashboard (Splunk)

## 📌 Project Overview
This project focuses on building a **Windows Security Monitoring Dashboard** using **Splunk Enterprise** to gain real-time visibility into **Windows Security Event Logs**. The dashboard helps monitor authentication activities, identify suspicious login behavior, and analyze user-related security events in a SOC-style environment.

The dashboard visualizes critical security metrics such as login attempts, failed access patterns, and user activity trends to support proactive security monitoring.

---

## 🎯 Objectives
- Monitor Windows authentication activities in real time
- Detect failed login attempts and abnormal access behavior
- Analyze login trends and user involvement
- Strengthen hands-on skills in SPL and dashboard design

---

## 🔍 Key Features
- **Total Login Attempts** (Successful + Failed)
- **Successful vs Failed Login Comparison**
- **Login Activity Over Time**
- **Top Users Involved in Local Group Membership Checks**

---

## 📊 Dashboard Visualizations & SPL Queries

### 1️⃣ Total Login Attempts
**Description:** Displays the total number of login attempts recorded in Windows Security Logs.

**SPL Query:**
```spl
index=main sourcetype=WinEventLog:Security (EventCode=4624 OR EventCode=4625)
| stats count as "Total Login Attempts"
Visualization Type:
📌 Single Value

2️⃣ Successful vs Failed Logins
Description: Compares successful and failed login attempts to quickly assess authentication health.

SPL Query:

spl
Copy code
index=main sourcetype=WinEventLog:Security
| eval Login_Status=case(EventCode=4624,"Successful", EventCode=4625,"Failed")
| stats count by Login_Status
Visualization Type:
📌 Pie Chart or Bar Chart

3️⃣ Login Activity Over Time
Description: Shows login trends over time to identify spikes or suspicious patterns.

SPL Query:

spl
Copy code
index=main sourcetype=WinEventLog:Security (EventCode=4624 OR EventCode=4625)
| timechart count
Visualization Type:
📌 Line Chart

4️⃣ Top Users – Local Group Membership Checks
Description: Identifies users frequently involved in local group membership-related activities.

SPL Query:

spl
Copy code
index=main sourcetype=WinEventLog:Security EventCode=4798
| stats count by Account_Name
| sort - count
| head 5
Visualization Type:
📌 Table or Bar Chart

🛠️ Tools & Technologies
Splunk Enterprise

Splunk Dashboard Studio

Search Processing Language (SPL)

Windows Security Event Logs

SOC Monitoring Concepts

💾 How to Save Dashboard & Visualizations (Dashboard Studio)
Go to Splunk → Dashboards

Click Create New Dashboard

Choose Dashboard Studio

Select Grid Layout (recommended for beginners)

Add a panel and paste the SPL query

Choose visualization type (Single Value, Pie, Line, Table)

Customize titles, colors, and labels

Click Save Dashboard

Set permissions (Private / Shared / App-level)

📈 Learning Outcomes
Hands-on experience with Windows Security Logs

Improved understanding of authentication-related event codes

Practical exposure to SPL queries and visual analytics

SOC-style approach to monitoring and threat detection

🚀 Future Enhancements
Configure alerts for multiple failed login attempts

Add geo-location-based login analysis

Integrate brute-force attack detection logic

📌 Conclusion
This project demonstrates the effective use of Splunk for real-time security monitoring by transforming raw Windows event data into actionable insights. It reflects a practical SOC use case and strengthens foundational skills required for cybersecurity and SIEM roles.
