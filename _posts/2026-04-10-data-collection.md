---
title: "Data Collection — Implementing System & Sensor Monitoring"
date: 2026-04-10 10:00:00 +0900
categories: Pipeline
tags: telegraf, hwinfo, python, influxdb
toc: true
---

## 🎯 Overview

In this post, we implement the **data collection layer**, which is the foundation of the entire monitoring system.

We collect two types of data:

- System metrics (CPU, Memory, Disk)
- Hardware sensor data (Temperature, Fan Speed, Power)

Due to platform limitations, we adopt a **hybrid collection strategy**.

---

## 🏗️ Data Collection Architecture

```bash
[System Metrics]
Telegraf (60s interval)
        ↓
InfluxDB

[Sensor Data]
HWiNFO → Python (3s interval)
        ↓
InfluxDB
```

---

## 📡 1. System Metrics Collection (Telegraf)

### Why Telegraf?
- Lightweight agent
- Native InfluxDB integration
- Supports Windows

### ⚙️ Telegraf Configuration
[agent]
  interval = "60s"

[[inputs.cpu]]
  percpu = true
  totalcpu = true

[[inputs.mem]]

[[inputs.disk]]

[[outputs.influxdb_v2]]
  urls = ["http://localhost:8086"]
  token = "YOUR_TOKEN"
  organization = "YOUR_ORG"
  bucket = "iot"

---

## 🌡️ 2. Sensor Data Collection (HWiNFO + Python)

### Why Not Telegraf?

Telegraf cannot collect:

- Temperature
- Fan Speed
- Power

### Solution

Use:

- HWiNFO (Sensor Provider)
- Python (Collector)

### ⚙️ HWiNFO Setup
Steps:
1. Run HWiNFO in Sensors-only mode
2. Enable:
  - Shared Memory Support

--- 

## 🧠 3. Hybrid Strategy Explained

| Data Type | Solution | Interval |
|--------|--------|
| CPU / Memory | Telegraf | 60s |
| Temperature | Python | 3s |
| Fan Speed | Python | 3s |

### ⚠️ Challenges
1. Windows Limitation
- No native API for sensors
- Requires external tool
  
2. Data Synchronization
- Different intervals
- Requires aggregation later
  
3. Performance
- High-frequency writes → InfluxDB tuning needed
  
### 🎯 Key Takeaways
1. Use Telegraf for standard metrics
2. Use Python for custom sensor ingestion
3. Separate pipelines for flexibility

---

### 🚀 Next Step

In the next post, we will design the data storage schema, including:

InfluxDB measurement design
MySQL aggregation tables
