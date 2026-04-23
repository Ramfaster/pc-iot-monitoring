---
title: "Conclusion — Lessons Learned and Future Directions"
date: 2026-04-17 10:00:00 +0900
categories: Conclusion
tags: retrospective, architecture, iot, monitoring
toc: true
---

## 🎯 Overview

This project started as a simple idea:

> Monitor PC hardware metrics.

However, it evolved into a **full data pipeline system** that includes:

- Data collection
- Processing
- Storage
- Alerting
- Analytics

---

## 🏗️ What We Built

```text

[Collection]
Telegraf + HWiNFO

[Processing]
Python Layer

[Storage]
InfluxDB + MySQL

[Alert]
Slack

[Analytics]
Metabase

```

---

## 🧠 Key Learnings

### 1. Monitoring is not just visualization

- Raw data alone has limited value
- Insight comes from processing and interpretation

---

### 2. Hybrid architecture is necessary

- No single tool solves everything
- Combining tools creates flexibility

---

### 3. Separation of concerns is critical

- Collection
- Processing
- Storage
- Analytics

Each layer must be independent

---

### 4. Real-world systems are messy

- Missing data
- Delays
- Unexpected failures

Design must account for imperfections

---

## ⚖️ Trade-offs

| Area | Decision |
|------|--------|
| Storage | InfluxDB + MySQL |
| Collection | Telegraf + Python |
| Alerts | Threshold + Anomaly |
| Frequency | 3s vs 60s |

---

## 📊 What Worked Well

- Clear separation between raw and aggregated data
- Simple but effective alert system
- Flexible Python processing layer
- Scalable architecture design

---

## ⚠️ Limitations

### 1. Single Node System

- Currently designed for one PC

---

### 2. Basic Anomaly Detection

- Uses simple statistical methods
- No machine learning yet

---

### 3. Manual Scaling

- No orchestration layer

---

## 🚀 Future Improvements

### 1. Multi-Node Support

```text

Multiple PCs → Centralized Pipeline

```

---

### 2. Advanced Anomaly Detection

- Machine learning models
- Predictive maintenance

---

### 3. Streaming Pipeline

- Kafka / message queue integration

---

### 4. Real-time Dashboard

- Combine Metabase with streaming tools

---

### 5. Container Orchestration

- Kubernetes-based deployment

---

## 🧠 Final Thoughts

This project demonstrates:

> A small monitoring idea can evolve into a full data engineering system.

It highlights the importance of:

- Architecture design
- Data flow understanding
- Operational thinking

---

## 🎯 Closing

If you followed this series, you now have:

- A complete monitoring pipeline
- A scalable architecture blueprint
- A foundation for advanced analytics systems

---

## 🙌 Thank You

Thank you for following this journey.

---
