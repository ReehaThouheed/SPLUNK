
# 🔐 Real-Time Detection of Failed Login Attempts Using Splunk

## 📌 Project Overview

This project demonstrates how **Splunk Enterprise** and **Splunk Universal Forwarder (UF)** can be used to collect **Windows Security Event Logs in real time** and detect multiple failed login attempts that may indicate a **brute-force or suspicious authentication attack**.

An alert is configured to trigger when a user enters the wrong password **three or more times within a short time window**. This project simulates a **real-world SOC (Security Operations Center)** use case for monitoring authentication-related threats.

---

## 🎯 Objectives

* Collect Windows Security logs in real time
* Detect failed login attempts (**Event ID 4625**)
* Identify suspicious behavior (≥ 3 failed attempts)
* Create an automated alert in Splunk
* Demonstrate practical SIEM monitoring

---

## 🛠️ Tools & Technologies Used

* **Splunk Enterprise**
* **Splunk Universal Forwarder**
* **Windows Event Viewer (Security Logs)**
* **SPL (Search Processing Language)**
* **Windows OS**

---

## 🧩 Architecture Overview

* Splunk Universal Forwarder collects Windows Security logs
* Logs are forwarded to Splunk Enterprise
* SPL queries analyze authentication failures
* Alerts notify when suspicious activity is detected

---

## 🚀 Step-by-Step Implementation

### 1️⃣ Install Splunk Enterprise

* Download from the official website:
  🔗 [https://www.splunk.com/en_us/download/splunk-enterprise.html](https://www.splunk.com/en_us/download/splunk-enterprise.html)
* Install using default settings
* Open Splunk at:

  ```
  http://localhost:8000
  ```
* Create admin credentials and complete setup

---

### 2️⃣ Install Splunk Universal Forwarder (UF)

* Download from:
  🔗 [https://www.splunk.com/en_us/download/universal-forwarder.html](https://www.splunk.com/en_us/download/universal-forwarder.html)
* Install on the same system (for local testing)
* Ensure the UF service is running

---

### 3️⃣ Configure Receiving Port in Splunk

* Navigate to:

  ```
  Settings → Forwarding and Receiving → Configure Receiving
  ```
* Click **New Receiving Port**
* Enter:

  * **IP Address:** `127.0.0.1`
  * **Port:** `9991`
* Save the configuration

---

### 4️⃣ Add Windows Security Logs as Data Input

* Navigate to:

  ```
  Settings → Data Inputs → Windows Event Logs
  ```
* Select **Security**
* Set:

  * **Index:** `main`
* Enable and save

This allows Splunk to ingest **Windows Security Event Logs**.

---

### 5️⃣ Verify Real-Time Log Collection

Open **Search & Reporting** and run:

```spl
index=main sourcetype=WinEventLog:Security
```

Set the time range to **Last 15 minutes** or **Realtime** to confirm logs are being collected live.

---

## 🚨 Detection Logic – Failed Login Attempts

### SPL Query Used

```spl
index=main sourcetype=WinEventLog:Security EventCode=4625
| bin _time span=5m
| stats count as failed_attempts by Account_Name, _time
| where failed_attempts >= 3
```

### Query Explanation

* `EventCode=4625` → Failed login attempts
* `bin _time span=5m` → Groups events into 5-minute windows
* `stats count` → Counts failures per user
* `where failed_attempts >= 3` → Detects suspicious behavior

---

## ⏰ Alert Configuration

* Click **Save As → Alert**
* Configure:

  * **Alert Name:** Multiple Failed Login Attempts
  * **Alert Type:** Scheduled
  * **Run Every:** 5 minutes
  * **Time Range:** Last 5 minutes
* Trigger condition:

  * **If number of results > 0**
* Save the alert

---

## 🧪 Practical Demonstration

* Lock the system using `Windows + L`
* Enter the wrong password **three times**
* Log in successfully
* Open **Splunk → Alerts**
* Verify that the alert has been triggered

---

## ✅ Results

* Real-time security logs collected successfully
* Failed login attempts detected automatically
* Alert triggered without manual intervention
* Demonstrates effective SIEM-based threat detection

---

## 📚 Key Learnings

* Understanding Windows Security Event IDs
* Real-time log ingestion using Universal Forwarder
* Writing SPL queries for security use cases
* Creating alerts for SOC monitoring
* Detecting brute-force login behavior

---

## 🔮 Future Enhancements

* Email or Slack alert notifications
* Dashboard visualization
* Detection of successful logins after failures
* Source IP–based brute-force detection
* MITRE ATT&CK mapping

---

## 👤 Author

**Reeha Thouheed**
Cybersecurity Enthusiast | SIEM | SOC | Splunk


