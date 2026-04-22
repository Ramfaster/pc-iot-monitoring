---
title: "Introduction — IoT PC Monitoring"
date: 2026-04-08 10:00:00 +0900
categories: Overview
tags: iot, monitoring, influxdb, hwinfo
---

## 🔍 Background

Modern operating systems provide basic visibility into system resources such as CPU, memory, and disk usage. However, **hardware-level telemetry**—including temperature, fan speed, and power consumption—is often hidden behind vendor-specific tools.

These tools are typically:

- UI-based and not programmatically accessible
- Not designed for long-term data storage
- Difficult to integrate into analytics pipelines

---

## ❗ Problem Statement

There is no unified system that can:

1. Collect both system metrics and hardware sensor data  
2. Handle different data collection intervals (seconds vs minutes)  
3. Store time-series data efficiently  
4. Trigger real-time alerts  
5. Provide analytical insights over time  

---

## 🎯 Objective

This project aims to build a **modular IoT-based monitoring platform** that:

- Collects:
  - CPU, Memory, Disk
  - Temperature, Fan Speed, Power

- Processes:
  - High-frequency sensor data (3 seconds)
  - Low-frequency system data (60 seconds)

- Delivers:
  - Real-time alerting (Slack)
  - Long-term analytics (Metabase)

---

## 🧠 Key Idea

> Monitoring is not the goal. **Insight is the goal.**

Instead of just visualizing data, the system focuses on:

- Detecting anomalies
- Identifying trends
- Enabling proactive responses

---

## 🏗️ System Overview

The architecture separates responsibilities into:

- Data Collection
- Processing Layer
- Time-Series Storage
- Alert System
- Analytics Layer

This ensures flexibility and scalability.

---

## 🚀 What’s Next

In the next post, we will define the **system requirements and data collection strategy**, including how to handle multi-rate data ingestion and hardware limitations.

---
