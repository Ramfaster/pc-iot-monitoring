---
title: "Architecture — IoT PC Monitoring System Design"
date: 2026-04-21 10:00:00 +0900
categories: Architecture
tags: architecture, pipeline, streaming
toc: true
---

## 🏗️ Overview

The system architecture is designed to separate data collection, processing, storage, and analytics.

---

## 🔄 Data Flow

HWiNFO → Python → InfluxDB
Telegraf → InfluxDB
InfluxDB → Slack / Metabase

---

## 🧩 Components

### 1. Telegraf
- Collects CPU, Memory, Disk
- Low-frequency (60s)

### 2. HWiNFO
- Provides hardware sensor data
- High-frequency (3s)

### 3. Python Layer
- Parses sensor data
- Sends to InfluxDB
- Triggers alerts

### 4. InfluxDB
- Time-series storage

### 5. Slack
- Real-time alerting

### 6. Metabase
- Analytics and visualization

---

## ⚖️ Design Decisions

### Why Hybrid Pipeline?
- Telegraf cannot collect hardware sensors
- Python required for custom ingestion

---

### Why InfluxDB?
- Optimized for time-series
- High write performance

---

### Why Slack Alerts?
- Lightweight and real-time

---

## 🚀 Next Step

We will implement the **data collection layer** in the next post.

---
