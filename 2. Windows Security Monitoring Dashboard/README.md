# 🔐 Windows Security Monitoring Dashboard (Splunk)

## 📌 Project Overview
This project involves building a Windows Security Monitoring Dashboard using Splunk Enterprise to analyze Windows Security Event Logs and provide real-time visibility into authentication activities. The dashboard helps identify login trends, failed access attempts, and user-related security events using a SOC-style monitoring approach.

---

## 🎯 Project Objectives
- Monitor Windows authentication activities in real time
- Identify failed login attempts and suspicious behavior
- Analyze login patterns and user activity
- Gain hands-on experience with SPL and Splunk dashboards

---

## 🔍 Dashboard Features & Visualizations

### 1️⃣ Total Login Attempts
**Description:**  
Displays the total number of login attempts, including both successful and failed logins.

```spl
index=main sourcetype=WinEventLog:Security (EventCode=4624 OR EventCode=4625)
| stats count as "Total Login Attempts"
```

**Visualization Type:**  
Single Value

---

### 2️⃣ Successful vs Failed Logins
**Description:**  
Compares successful and failed login attempts to quickly assess authentication health.

```spl
index=main sourcetype=WinEventLog:Security
| eval Login_Status=case(EventCode=4624,"Successful", EventCode=4625,"Failed")
| stats count by Login_Status
```

**Visualization Type:**  
Pie Chart or Bar Chart

---

### 3️⃣ Login Activity Over Time
**Description:**  
Shows login trends over time to identify spikes or suspicious patterns.

```spl
index=main sourcetype=WinEventLog:Security (EventCode=4624 OR EventCode=4625)
| timechart count
```

**Visualization Type:**  
Line Chart

---

### 4️⃣ Top Users – Local Group Membership Checks
**Description:**  
Identifies users frequently involved in local group membership-related activities.

```spl
index=main sourcetype=WinEventLog:Security EventCode=4798
| stats count by Account_Name
| sort - count
| head 5
```

**Visualization Type:**  
Table or Bar Chart

---

## 🛠️ Tools & Technologies
- Splunk Enterprise
- Splunk Dashboard Studio
- Search Processing Language (SPL)
- Windows Security Event Logs
- SOC Monitoring Concepts

---

## 💾 How to Create & Save the Dashboard (Dashboard Studio)
1. Go to Splunk → Dashboards
2. Click Create New Dashboard
3. Choose Dashboard Studio
4. Select Grid Layout
5. Add panels and paste SPL queries
6. Choose visualization types (Single Value, Pie, Line, Table)
7. Customize titles, colors, and labels
8. Click Save Dashboard
9. Set permissions (Private / Shared / App-level)

---

## 📈 Learning Outcomes
- Hands-on experience with Windows Security Logs
- Understanding of authentication-related event codes
- Practical exposure to SPL queries and visual analytics
- SOC-style monitoring and threat detection experience

---

## 🚀 Future Enhancements
- Configure alerts for multiple failed login attempts
- Add geo-location-based login analysis
- Implement brute-force attack detection logic

---

## 📌 Conclusion
This project demonstrates how Splunk can be used as a SIEM tool to transform raw Windows Security Event Logs into actionable insights through dashboards and SPL queries.
