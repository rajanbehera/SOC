# SIEM Architecture

## Security Information and Event Management — Study Notes

### Security Operations Center (SOC) Notes

**Created By: Mr. Rajan**

---

# 01 — What is SIEM?

## Definition

**SIEM (Security Information and Event Management)** is a security platform that combines:

- **SIM (Security Information Management)**
- **SEM (Security Event Management)**

A SIEM collects, stores, normalizes, correlates, and analyzes logs from an organization's infrastructure in real time.

### Main Objectives

- Threat Detection
- Incident Investigation
- Compliance Monitoring
- Security Visibility
- Centralized Log Management

---

# 02 — Core Architecture Layers

| Layer | Name | Description |
| ------- | ------------------------------ | --------------------------------------------------------- |
| Layer 5 | Presentation & Dashboards | Visualization, alerting, reporting, ticketing integration |
| Layer 4 | Analytics & Correlation Engine | Detection rules, UEBA, threat intelligence matching |
| Layer 3 | Storage & Indexing | Data storage, search indexes, retention |
| Layer 2 | Normalization & Parsing | Parsing, field extraction, schema mapping |
| Layer 1 | Data Collection | Log collection from all sources |

---

## Author

**Created By: Mr. Rajan**
