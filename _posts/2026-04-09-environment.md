---
title: "Environment Setup — Building the Foundation for IoT PC Monitoring"
date: 2026-04-09 10:00:00 +0900
categories: Environment
tags: Rocky, podman, influxdb, mysql, telegraf, HWiNFO, grafana, metabase, slack
toc: true
---

## 🎯 Overview

Before implementing the monitoring system, we need to establish a **stable and reproducible environment**.

This includes:

- Operating system setup
- Container runtime configuration
- Database installation
- Monitoring tools preparation

---

## 🖥️ System Environment

### OS
- Windows 11 (Data Collection Node)
- Rocky Linux (Container Host)

---

## 📦 Container Platform

We use:

- Podman (instead of Docker)

### Why Podman?

- Daemonless architecture
- Better security model
- Compatible with Docker CLI

---

## 🗄️ Data Infrastructure

### 1. InfluxDB (Time-Series Database)

Used for:

- High-frequency sensor data
- Real-time metric storage

---

### 2. MySQL (Relational Database)

Used for:

- Aggregated data
- Reporting and analytics

---

### 3. Redis (Optional)

Used for:

- Caching
- Real-time processing buffer

---

## 📡 Data Collection Tools

### 1. Telegraf

Used for:

- CPU / Memory / Disk collection
- Low-frequency metrics (60s)

---

### 2. HWiNFO

Used for:

- Temperature
- Fan Speed
- Power consumption

---

## 🧠 Processing Layer

### Python

Used for:

- Sensor data parsing
- Data transformation
- Alert triggering

---

## 🔔 Alert System

### Slack Webhook

Used for:

- Real-time notifications
- Threshold-based alerts

---

## 📊 Analytics Layer

### Metabase

Used for:

- Dashboard visualization
- KPI analysis

---

## 🏗️ Environment Architecture

Windows (HWiNFO + Telegraf)
↓
Python Processing Layer
↓
InfluxDB / MySQL
↓
Slack / Metabase


---

## 🚀 Next Step

In the next post, we will implement the **data collection layer**, starting with Telegraf configuration and HWiNFO integration.

---
