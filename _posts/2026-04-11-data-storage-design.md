---
title: "Data Storage Design — Structuring Time-Series and Analytical Data"
date: 2026-04-11 10:00:00 +0900
categories: Architecture
tags: influxdb, mysql, schema-design, time-series
toc: true
---

## 🎯 Overview

In a monitoring system, **how data is stored** directly impacts:

- Query performance
- Storage efficiency
- Insight generation capability

This post defines a **dual-storage strategy** using:

- InfluxDB → raw time-series data
- MySQL → aggregated analytical data

---

## 🏗️ Storage Architecture

```text
[Data Collection Layer]
   ├─ Telegraf
   └─ Python (HWiNFO)

        ↓

[InfluxDB] (Raw Data)
        ↓
[Aggregation Layer]
        ↓
[MySQL] (Analytics Data)
        ↓
[Metabase / Dashboard]
```

## 🧠 Design Strategy

#### Why Two Databases?

| Database | Role |
|--------|--------|
| InfluxDB | High-frequency raw data |
| MySQL | Aggregated / reporting |

### 1. InfluxDB Schema Design

1. Measurement

- system_metrics
- hwinfo_metrics

2. Tag vs Field

| Type | Usage |
|--------|--------|
| Tag | filter / grouping |
| Field | actual value |

3. Recommended Schema
❗ Do NOT store numeric values as tags

**system_metrics**
```text
measurement: system_metrics
tags:
  - host
fields:
  - cpu_usage
  - mem_usage
  - disk_usage
```

**hwinfo_metrics**
```text
measurement: hwinfo_metrics
tags:
  - host
fields:
  - cpu_temp
  - fan_speed
  - power
```

### 🧪 Example Data (Line Protocol)
```text
system_metrics,host=pc-01 cpu_usage=25.3,mem_usage=60.2
hwinfo_metrics,host=pc-01 cpu_temp=55.2,fan_speed=1200
```

### 🕒 Retention Policy

- High-frequency data grows fast
- Storage cost increases

| Data Type | Retention |
|--------|--------|
| Raw sensor data | 7~30 days |
| Aggregated data | long-term |

### 📊 Downsampling Strategy

Example:
```text
Raw: 3 sec interval
Downsample: 1 min avg
```

---

## 🗄️ 2. MySQL Schema Design

**Purpose**
- Store aggregated metrics
- Enable BI queries (Metabase)

### 1. 🔄 Aggregation Flow

```text
InfluxDB (raw)
        ↓
Python Aggregation
        ↓
MySQL (summary)
```
---

### 2. 🧠 Design Decisions

#### 1. Separation of Raw vs Aggregated Data
- InfluxDB → fast writes
- MySQL → fast queries

#### 2. Avoid Heavy Queries in InfluxDB
- Complex analytics → MySQL

#### 3. Optimize for Read vs Write

| System | Optimization |
|--------|--------|
| InfluxDB | write-heavy |
| MySQL | read-heavy |

#### 4. Common Mistakes

❌ Using only MySQL
→ Poor performance for time-series

❌ Using only InfluxDB
→ Poor BI support

❌ Wrong tag design
→ Query performance drop

---

### 3. 🎯 Key Takeaways

- Use InfluxDB for ingestion
- Use MySQL for analytics
- Separate concerns clearly

--- 

🚀 Next Step

In the next post, we will implement the data pipeline and aggregation logic, including:

- Python aggregation jobs
- Scheduling strategy
- Data transformation

---
