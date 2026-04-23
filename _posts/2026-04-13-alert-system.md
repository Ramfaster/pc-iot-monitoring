---
title: "Alert System — Real-time Monitoring with Slack and Anomaly Detection"
date: 2026-04-13 10:00:00 +0900
categories: Analytics
tags: alert, slack, anomaly-detection, monitoring
toc: true
---

## 🎯 Overview

Collecting and storing data is not enough.  
The real value of a monitoring system comes from **real-time alerts and anomaly detection**.

This post implements:

- Slack-based alert notifications
- Threshold-based alert rules
- Basic anomaly detection strategy

---

## 🏗️ Alert System Architecture

```text

[InfluxDB (Raw Data)]
        ↓
[Python Alert Engine]
        ↓
[Slack Webhook]
        ↓
[User Notification]

```

---

## 🧠 Alert Strategy

We define two types of alerts:

### 1. Threshold-based Alerts
- Simple and predictable
- Example:
  - CPU Temperature > 80°C
  - Fan Speed < 500 RPM

---

### 2. Anomaly-based Alerts
- Detect abnormal patterns
- Based on statistical deviation

---

## 📡 Slack Integration

### Why Slack?

- Real-time notification
- Easy integration (Webhook)
- Lightweight and flexible

---

### Webhook Setup

1. Create Slack App
2. Enable Incoming Webhook
3. Copy Webhook URL

---

### Example Message Format

```text

🔥 ALERT: High CPU Temperature  
Host: pc-01  
Value: 85°C  

```

---

## 🐍 Python Alert Engine

### Workflow

```text

1. Fetch latest data from InfluxDB
2. Evaluate threshold rules
3. Detect anomalies
4. Send alert to Slack

```

---

## 🔥 Threshold-based Detection

### Example Rules

| Metric | Condition |
|------|----------|
| CPU Temp | > 80°C |
| Fan Speed | < 500 RPM |
| Power | > 120W |

---

### Logic

```text

if cpu_temp > 80:
    trigger_alert()

```

---

## 📊 Anomaly Detection (Basic)

### Method: Z-Score

Z-score measures how far a value is from the average.

---

### Formula

```text

Z = (X - μ) / σ

```

---

### Interpretation

| Z-Score | Meaning |
|--------|--------|
| 0 ~ 2 | Normal |
| > 3 | Anomaly |

---

### Example Logic

```text

if z_score > 3:
    trigger_alert()

```

---

## 🧠 Combining Alerts

We combine both methods:

- Threshold → Immediate alerts
- Anomaly → Smart alerts

---

## ⏱️ Alert Frequency Control

### Problem

- Too many alerts → noise
- Too few alerts → missed issues

---

### Solution

- Cooldown period (e.g. 5 minutes)
- Deduplication logic

---

### Example

```text

if last_alert < 5 minutes ago:
    skip_alert()

```

---

## 🧪 Example Alert Flow

```text

1. Read latest temperature
2. Check threshold
3. Calculate Z-score
4. If triggered → send Slack message

```

---

## ⚠️ Challenges

### 1. False Positives

- Temporary spikes
- Need smoothing

---

### 2. Alert Flooding

- Repeated alerts
- Requires throttling

---

### 3. Data Delay

- Late ingestion
- Impacts real-time alerts

---

## 🎯 Best Practices

- Use threshold + anomaly together
- Add cooldown logic
- Keep messages simple and clear

---

## 📊 Example Alert Message

```text

🔥 ALERT: Temperature Spike  
Host: pc-01  
Temp: 87°C  
Status: Critical  

```

---

## 🚀 Next Step

In the next post, we will build the **Analytics & Dashboard layer**, including:

- KPI design
- Metabase dashboard
- Insight visualization

---
