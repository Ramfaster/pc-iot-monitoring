---
title: "Environment Setup — Building the Foundation for IoT PC Monitoring"
date: 2026-04-09 10:00:00 +0900
categories: Environment
tags: Rocky, podman, influxdb, mysql, telegraf, HWiNFO, grafana, metabase, slack
toc: true
---

## 🎯 Overview

Before implementing the monitoring system, we need to establish a **stable and reproducible environment**.
A monitoring system is only as reliable as its environment.  
This post defines a **reproducible and production-like setup** for building an IoT-based PC monitoring platform.

This includes:

- Operating system setup
- Container runtime configuration
- Database installation
- Monitoring tools preparation

focus on:

- Separation of concerns
- Container-based deployment
- Hybrid data collection strategy

---

## 🖥️ System Environment

Below is the environment-level architecture:

```bash
[Windows 11]
├─ HWiNFO (Sensor Data)
├─ Telegraf (System Metrics)
└─ Python (Processing)
 ↓
[Rocky Linux + Podman]
├─ InfluxDB
├─ MySQL
├─ Redis (optional)
└─ Metabase
 ↓
[Slack Alert + Dashboard]

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

### 🧱 1. Operating System Setup

#### Windows 11 (Data Collection Node)

Used for:
- Hardware sensor extraction
- System metric collection

Key constraint:
> Windows does not provide native APIs for temperature or fan speed.

---

#### Rocky Linux (Container Host)

Used for:
- Running databases and analytics tools
- Stable server-side processing

---

### 📦 2. Container Platform — Podman

#### Why Podman?

| Feature | Benefit |
|--------|--------|
| Daemonless | No background service required |
| Rootless | Improved security |
| Docker-compatible | Easy migration |

---

### Installation (Rocky Linux)

sudo dnf install -y podman
podman --version

---

### 🗄️ 3. InfluxDB (Time-Series Core) / MySQL

InfluxDB Initial Setup
Organization
Bucket (e.g. iot)
API Token

MySQL Role of MySQL
Store aggregated data
Support BI tools (Metabase)

---

### 🌡️ 4. HWiNFO Setup (Sensor Data)

Why HWiNFO?
- Provides access to:
  - CPU Temperature
  - Fan Speed
  - Power Consumption
 
Configuration
- Run in Sensors-only mode
- Enable:
  - Shared Memory Support

Multi-Rate Data Ingestion

| Type | Interval |
|--------|--------|
| Sensor | 3 sec |
| System | 60 sec |

---

## 🚀 Next Step

In the next post, we will implement the **data collection layer**, starting with Telegraf configuration and HWiNFO integration.

- Telegraf configuration
- HWiNFO integration
- Python collector

---
