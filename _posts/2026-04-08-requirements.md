---
title: "Requirements — Designing an IoT-Based PC Monitoring System"
date: 2026-04-08 10:00:00 +0900
categories: Requirements
tags: iot, system-design, monitoring
toc: true
---

## 🎯 Overview

Before building the system, it is essential to define clear **functional and non-functional requirements**.

---

## 📊 Functional Requirements

### 1. System Metrics Collection
- CPU usage
- Memory usage
- Disk I/O

### 2. Hardware Sensor Collection
- Temperature (CPU, GPU)
- Fan speed (RPM)
- Power consumption

---

### 3. Multi-Rate Data Ingestion

| Metric Type | Interval |
|------------|--------|
| Temperature / Fan | 3 seconds |
| CPU / Memory / Disk | 60 seconds |

---

### 4. Data Storage

- Time-series storage (InfluxDB)
- Aggregated storage (MySQL)

---

### 5. Alert System

- Slack notification
- Threshold-based triggers
- Future: anomaly detection

---

## ⚙️ Non-Functional Requirements

### Performance
- Handle high-frequency ingestion
- Low latency alerting

### Reliability
- No data loss
- Stable data pipeline

### Scalability
- Support multi-PC architecture (future)

---

## 🧠 Design Challenges

### 1. Windows Limitation
- No native API for fan/temp
- Requires external tools (HWiNFO)

### 2. Hybrid Data Pipeline
- Combining Telegraf + Python

### 3. Data Volume
- High-frequency sensor data → storage impact

---

## 🏗️ Design Strategy

- Separate system metrics and sensor metrics
- Use different ingestion pipelines
- Normalize data before storage

---

## 🚀 Next Step

In the next post, we will design the **system architecture and data pipeline**.

---
