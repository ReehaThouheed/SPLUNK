# 📊 Instagram Reel Metrics Dashboard using Splunk

## 🔍 Project Overview
This project presents an **Instagram Reel Analytics Dashboard** built using **Splunk Enterprise**. The dashboard visualizes key engagement metrics such as total views, viewer types, audience demographics, geographic distribution, and interaction sources. The goal is to convert raw Instagram engagement data into meaningful insights using **SPL (Search Processing Language)** and interactive visualizations.

---

## 🎯 Objectives
- Analyze Instagram Reel performance using log/CSV-based data  
- Understand audience behavior and demographics  
- Visualize engagement metrics in an interactive Splunk dashboard  
- Gain hands-on experience with SPL queries and dashboard creation  

---

## 🛠️ Tools & Technologies Used
- **Splunk Enterprise**
- **SPL (Search Processing Language)**
- **CSV Data Source** (`Insta_analysis.csv`)
- **Dashboard Studio / Classic Dashboards**

---

## 📂 Data Description
The dataset contains Instagram Reel interaction data with fields such as:
- `views`
- `event_type` (like, share, save, view)
- `viewer_type` (Follower / Non-Follower)
- `gender`
- `age_group`
- `country`
- `source` (Feed, Explore, Profile)

---

## 📈 Dashboard Features

### 🔹 Total Views
~~~spl
index="main" source="instagram_reel_simulated_logs.csv" sourcetype="csv" event_type="View"
| stats count
~~~

---

### 🔹 Viewer Type Distribution (Followers vs Non-Followers)
~~~spl
index=main sourcetype=csv extracted_source=Reels
| eval viewer_type = if('Type of viewer'="Follower","Followers","Non-Followers")
| stats count BY viewer_type
~~~

---

### 🔹 Nation of Audience
~~~spl
index=main sourcetype=csv extracted_source=Reels
| stats count AS viewers BY country
~~~

---

### 🔹 Geo-Location of Audience
~~~spl
index=main sourcetype=csv extracted_source=Reels
| stats count AS viewers BY country
| geom geo_countries featureIdField=country
~~~

---

### 🔹 Age Group of Audience
~~~spl
index=main sourcetype=csv extracted_source=Reels
| stats count AS "Number of views" BY age_group
~~~

---

### 🔹 Gender Distribution of Audience
~~~spl
index=main sourcetype=csv extracted_source=Reels
| eval Gender = if('gender'="M","Male","Female")
| stats count BY Gender
~~~

---

### 🔹 Event Type Analysis (Likes, Shares, Saves, Views)
~~~spl
index=main sourcetype=csv extracted_source=Reels
| stats count AS "Event Count" BY event_type
~~~

---

### 🔹 Source of Views
~~~spl
source="Insta_analysis.csv"
| stats count AS view_count BY extracted_source
~~~

---

### 🔹 Likes by Gender and Viewer Type
~~~spl
index=main sourcetype=csv extracted_source=Reels
| eval Gender = if('gender'="M","Male","Female")
| stats count BY Gender
~~~

---
## 🧭 Create the Dashboard (One-Time Setup)

1. Open **Splunk Enterprise** and type these spl commands
2. Go to **Dashboards → Create New Dashboard**
3. Choose **Dashboard Studio** (recommended for modern UI)
4. Set the **Dashboard Title** as:  
   **📊 Instagram Reel Metrics & Audience Analytics**
5. Add a **Description** (optional but professional):  
   *An interactive dashboard analyzing Instagram Reel engagement, audience demographics, and traffic sources using Splunk.*
6. Select **Layout: Grid** (easy to manage and resize panels)
7. Click **Create Dashboard**

Once the dashboard is created, add **one panel per metric** as described below.

---

## 📈 Panel-wise Visualization Guide

### 1️⃣ Total Views
- **Purpose:** Show overall reach at a glance  
- **Visualization:** Single Value  
- **Why:** Best for highlighting one important KPI  
- **Panel Title:** Total Reel Views  

---

### 2️⃣ Viewer Type Distribution (Followers vs Non-Followers)
- **Purpose:** Compare follower vs non-follower reach  
- **Visualization:** Pie Chart  
- **Why:** Clearly shows proportion/share  
- **Panel Title:** Follower vs Non-Follower Views  

---

### 3️⃣ Nation of Audience
- **Purpose:** Compare views by country  
- **Visualization:** Bar Chart (Horizontal)  
- **Why:** Easy country-wise comparison  
- **Panel Title:** Top Countries by Views  
- **X-axis:** Views  
- **Y-axis:** Country  

---

### 4️⃣ Geo-Location of Audience
- **Purpose:** Visual geographic spread  
- **Visualization:** Choropleth Map  
- **Why:** Best for country-based audience mapping  
- **Panel Title:** Global Audience Distribution  

---

### 5️⃣ Age Group of Audience
- **Purpose:** Understand which age group engages most  
- **Visualization:** Bar Chart  
- **Why:** Age groups are categorical and comparable  
- **Panel Title:** Audience Age Group Distribution  

---

### 6️⃣ Gender Distribution of Audience
- **Purpose:** Compare male vs female engagement  
- **Visualization:** Pie Chart  
- **Why:** Simple gender split visualization  
- **Panel Title:** Gender Distribution of Audience  

---

### 7️⃣ Event Type Analysis (Likes, Shares, Saves, Views)
- **Purpose:** Analyze engagement actions  
- **Visualization:** Column Chart  
- **Why:** Shows interaction intensity per event  
- **Panel Title:** Engagement by Event Type  

---

### 8️⃣ Source of Views
- **Purpose:** Identify where traffic comes from  
- **Visualization:** Bar Chart  
- **Why:** Clear comparison between Feed, Explore, and Profile  
- **Panel Title:** Source of Reel Views  

---

### 9️⃣ Likes by Gender and Viewer Type
- **Purpose:** Deep engagement analysis  
- **Visualization:** Stacked Bar Chart  
- **Why:** Shows combined relationship clearly  
- **Panel Title:** Likes by Gender & Viewer Type  

## 📊 Key Insights
- Majority of views originated from **Non-Followers**, indicating higher organic reach  
- **India** contributed the highest number of views  
- Younger age groups showed stronger engagement  
- Feed and Explore pages were the major sources of traffic  
- Female audience engagement was slightly higher than male audience  

---

## 🚀 Conclusion
This project demonstrates how **Splunk Enterprise** can be effectively used for **social media analytics** beyond traditional log monitoring. By leveraging **SPL** and interactive dashboards, Instagram Reel performance can be analyzed efficiently to understand audience behavior and engagement patterns.

This dashboard is useful for **digital marketers, analysts, and data enthusiasts** seeking actionable insights from social media data.
