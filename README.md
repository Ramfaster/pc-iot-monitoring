# 🚀 IoT PC Monitoring & Insight Platform

![GitHub repo size](https://img.shields.io/github/repo-size/ramfaster/pc-iot-monitoring)
![GitHub last commit](https://img.shields.io/github/last-commit/ramfaster/pc-iot-monitoring)
![GitHub stars](https://img.shields.io/github/stars/ramfaster/pc-iot-monitoring?style=social)

---

## 📌 Overview

A real-time monitoring and analytics platform that transforms **raw PC hardware metrics into actionable insights**.

---

## 🎥 Demo

👉 Live Blog  
https://ramfaster.github.io/pc-iot-monitoring/

---

## 🏗️ Architecture

```text

[Windows]
  ├─ Telegraf
  ├─ HWiNFO
  └─ Python

        ↓

[InfluxDB]
        ↓
[MySQL]
        ↓
[Slack / Metabase]

```

---

## 🧠 Key Features

- Real-time system monitoring
- Hardware sensor integration
- Hybrid data pipeline
- Slack alert system
- BI dashboard (Metabase)

---

## 📊 Dashboard Preview

![Dashboard](/assets/img/metabase-dashboard.png)

---

## ⚙️ Tech Stack

- Python
- InfluxDB
- MySQL
- Telegraf
- HWiNFO
- Slack
- Metabase

---

## 🚀 Getting Started

```text

1. Install dependencies
2. Run Telegraf
3. Start Python collector
4. Access InfluxDB & Metabase

```

---

## 📚 Documentation

👉 https://ramfaster.github.io/pc-iot-monitoring/

---

## 🎯 Goal

Transform monitoring into insight-driven decision making.

---

## 📄 License

MIT
