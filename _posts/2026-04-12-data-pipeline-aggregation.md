---
title: "Data Pipeline & Aggregation — Implementing Data Flow with Python"
date: 2026-04-12 10:00:00 +0900
categories: Pipeline
tags: python, pipeline, aggregation, influxdb, mysql
toc: true
---

## 🎯 Overview

After designing data storage, the next step is building the **data pipeline** that connects:

- Data collection
- Data storage
- Data aggregation
- Data delivery

This post focuses on implementing the **Python-based processing layer**.

---

## 🏗️ Data Pipeline Architecture

```text

[Telegraf / HWiNFO]
        ↓
[InfluxDB (Raw Data)]
        ↓
[Python Aggregation Layer]
        ↓
[MySQL (Summary Data)]
        ↓
[Metabase / Analytics]

```

---

## 🧠 Pipeline Responsibilities

The Python layer is responsible for:

- Reading raw data from InfluxDB
- Transforming data into meaningful metrics
- Aggregating data (hourly / daily)
- Storing results in MySQL
- Triggering alerts (optional)

---

## 🔄 Data Flow

### Step 1 — Data Ingestion

- Telegraf → system metrics
- Python → sensor metrics
- Stored in InfluxDB

---

### Step 2 — Data Aggregation

- Read data from InfluxDB
- Apply aggregation logic
- Store in MySQL

---

## 📡 InfluxDB Query Strategy

We query time ranges such as:

- Last 1 hour
- Last 1 day

---

### Example Query Concept

```text

SELECT mean(cpu_usage)
FROM system_metrics
WHERE time > now() - 1h
GROUP BY time(1m)

```

---

## 🧮 Aggregation Logic

### Key Metrics

- Average CPU usage
- Maximum temperature
- Average power
- Anomaly count

---

### Aggregation Rules

| Metric | Method |
|------|------|
| CPU | AVG |
| Temperature | MAX |
| Power | AVG |
| Anomaly | COUNT |

---

## 🐍 Python Aggregation Design

### Core Steps

1. Fetch data from InfluxDB
2. Process data
3. Insert into MySQL

---

### Python Workflow

```text

1. connect_influx()
2. query_data()
3. calculate_metrics()
4. insert_mysql()

```

---

## 🗄️ MySQL Insert Strategy

### Target Tables

- device_summary_hourly
- device_summary_daily

---

### Insert Concept

```text

INSERT INTO device_summary_hourly (...)

```

---

## ⏱️ Scheduling Strategy

### Options

| Method | Description |
|------|------------|
| Cron | Linux scheduler |
| Task Scheduler | Windows |
| Python loop | Simple approach |

---

### Recommended

- Hourly aggregation → every 1 hour
- Daily aggregation → once per day

---

## 🔁 Example Pipeline Cycle

```text

Every 1 hour:
  - Fetch last 1 hour data
  - Calculate averages
  - Store in MySQL

Every 1 day:
  - Fetch daily data
  - Calculate summaries
  - Store results

```

---

## ⚠️ Challenges

### 1. Data Delay

- Data may arrive late
- Use buffer window

---

### 2. Missing Data

- Handle NULL values
- Use fallback logic

---

### 3. Time Alignment

- Ensure consistent timestamps

---

## 🎯 Key Design Decisions

### 1. Batch over Real-time Aggregation

- Simpler
- More stable

---

### 2. Separation of Concerns

- Collection → InfluxDB
- Aggregation → Python
- Analytics → MySQL

---

### 3. Idempotent Processing

- Avoid duplicate inserts
- Use unique keys

---

## 📊 Pipeline Benefits

- Reduced query load on InfluxDB
- Faster analytics queries
- Clean separation of raw vs processed data

---

## 🚀 Next Step

In the next post, we will implement:

- Real-time alert system
- Slack integration
- Threshold-based monitoring

---
