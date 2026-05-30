
# SIEM Architecture
## Security Information and Event Management (SIEM)
### Security Operations Center (SOC) Study Notes

**Created By: Mr. Rajan**

---

# Table of Contents

1. What is SIEM
2. Core Architecture Layers
3. Data Flow Pipeline
4. Key Data Sources
5. Collection Methods
6. Normalization & Common Schemas
7. Correlation & Detection Techniques
8. Storage Architecture
9. Popular SIEM Platforms
10. SIEM + SOAR Integration
11. Key SIEM Metrics
12. Deployment Models

---

# 01 — What is SIEM?

## Definition

Security Information and Event Management (SIEM) is a centralized security platform that collects, aggregates, normalizes, stores, correlates, and analyzes security logs from multiple devices and applications.

SIEM combines:

- Security Information Management (SIM)
- Security Event Management (SEM)

## Objectives

- Centralized Log Collection
- Threat Detection
- Incident Investigation
- Compliance Monitoring
- Threat Hunting
- Security Visibility

## Why Organizations Need SIEM

- Millions of logs are generated daily.
- Manual analysis is impossible.
- SIEM automates detection and monitoring.
- Enables faster response to cyber attacks.

---

# 02 — Core Architecture Layers

## Layer 1 — Data Collection

Responsible for collecting logs from various sources.

Sources include:

- Firewalls
- Routers
- Switches
- IDS/IPS
- Windows Servers
- Linux Servers
- EDR Solutions
- Applications
- Cloud Platforms

## Layer 2 — Parsing & Normalization

Converts different log formats into a common structure.

Activities:

- Parsing
- Field Extraction
- Timestamp Correction
- Data Validation
- Deduplication

## Layer 3 — Storage & Indexing

Stores logs and creates searchable indexes.

Benefits:

- Fast Search
- Historical Analysis
- Threat Hunting

## Layer 4 — Analytics & Correlation

Detects suspicious activity.

Functions:

- Correlation Rules
- Behavioral Analytics
- Threat Intelligence Matching
- Risk Scoring

## Layer 5 — Dashboards & Reporting

Provides:

- Dashboards
- Reports
- Alerts
- Investigations
- Compliance Reports

---

# 03 — SIEM Data Flow Pipeline

```text
Log Source
    ↓
Collector
    ↓
Parser
    ↓
Normalizer
    ↓
Indexer
    ↓
Correlation Engine
    ↓
Alert
    ↓
SOC Analyst
```

## Explanation

### Log Source

Generates security events.

### Collector

Receives logs from multiple devices.

### Parser

Breaks raw logs into fields.

### Normalizer

Converts logs into common schema.

### Indexer

Makes data searchable.

### Correlation Engine

Applies detection logic.

### Alerting

Creates incidents for analysts.

---

# 04 — Key Data Sources

## Network Devices

### Firewalls

Provide:

- Allowed Traffic
- Blocked Traffic
- Threat Logs

### Routers

Provide:

- Traffic Information
- Interface Status

### IDS/IPS

Provide:

- Attack Signatures
- Intrusion Alerts

## Endpoints

### Windows Logs

- Security Logs
- System Logs
- Application Logs

### Linux Logs

- Syslog
- Auditd
- Auth Logs

### EDR Telemetry

- Process Creation
- File Modifications
- Malware Activity

## Identity Sources

- Active Directory
- LDAP
- RADIUS
- SSO

## Cloud Sources

### AWS

- CloudTrail
- CloudWatch

### Azure

- Azure Monitor
- Activity Logs

### Google Cloud

- Audit Logs

## Threat Intelligence

Examples:

- Malicious IPs
- Domains
- URLs
- File Hashes

---

# 05 — Collection Methods

## Agent-Based Collection

Examples:

- Splunk UF
- Wazuh Agent
- Elastic Agent
- Filebeat

Advantages:

- Reliable
- Detailed Telemetry
- Secure Communication

## Syslog Collection

Protocols:

- UDP 514
- TCP 514

Common Devices:

- Firewalls
- Routers
- Switches

## API Collection

Used for:

- Microsoft 365
- AWS
- Azure
- Okta

## Network TAP / SPAN

Provides:

- Network Visibility
- Flow Analysis
- Metadata Collection

---

# 06 — Normalization & Common Schemas

## Why Normalization is Important

Different vendors use different field names.

Normalization converts all events into a standard format.

## CEF

Common Event Format

```text
CEF:Version|Vendor|Product|Version|EventID|Name|Severity|Extension
```

## LEEF

Log Event Extended Format

Used mainly by QRadar.

## ECS

Elastic Common Schema

Examples:

```text
source.ip
destination.ip
event.action
user.name
```

## OCSF

Open Cybersecurity Schema Framework

Benefits:

- Vendor Neutral
- Easier Integrations
- Better Portability

---

# 07 — Correlation & Detection Techniques

## Rule-Based Detection

Example:

```text
5 Failed Logins
within 60 seconds
from same IP
= Alert
```

### Types

- Threshold Rules
- Sequence Rules
- Join Rules

## UEBA

User and Entity Behavior Analytics

Detects:

- Abnormal Login Times
- Insider Threats
- Data Exfiltration

## Threat Intelligence Matching

Checks:

- IP Reputation
- Domain Reputation
- Malware Hashes

## MITRE ATT&CK Mapping

Maps detections to attacker techniques.

Benefits:

- Better Coverage
- Threat Hunting
- Detection Validation

---

# 08 — Storage Architecture

## Hot Storage

Retention:

- 7–30 Days

Characteristics:

- SSD/NVMe
- Fast Searches

## Warm Storage

Retention:

- 30–90 Days

Characteristics:

- Lower Cost
- Indexed Data

## Cold Storage

Retention:

- 90 Days to 7 Years

Characteristics:

- Archive Storage
- Compliance Retention

## Storage Estimation

Formula:

```text
EPS × Average Event Size × Retention Days
```

Example:

1000 EPS × 500 Bytes × 30 Days

Used for sizing SIEM deployments.

---

# 09 — Popular SIEM Platforms

## Splunk Enterprise Security

Features:

- SPL Queries
- Strong Ecosystem
- Enterprise Scale

## Microsoft Sentinel

Features:

- Cloud Native
- KQL Queries
- Built-in SOAR

## Elastic Security

Features:

- Open Source Core
- ECS Support
- Flexible Deployment

## IBM QRadar

Features:

- Strong Correlation
- LEEF Support

## Exabeam

Features:

- UEBA Focused
- Smart Timelines

## Wazuh

Features:

- Open Source
- XDR Functions
- Community Driven

---

# 10 — SIEM + SOAR Integration

## What is SOAR

Security Orchestration, Automation and Response.

Workflow:

```text
SIEM Detection
      ↓
SOAR Playbook
      ↓
Automated Response
```

## Automated Actions

- Block IP
- Disable User
- Isolate Endpoint
- Create Ticket
- Send Notification

## Benefits

- Faster Response
- Reduced Workload
- Consistent Actions

---

# 11 — Key SIEM Metrics

## EPS

Events Per Second

Measures ingestion capacity.

## MTTD

Mean Time To Detect

Measures detection speed.

## MTTR

Mean Time To Respond

Measures response speed.

## False Positive Rate

Percentage of incorrect alerts.

## Alert Fidelity

Percentage of useful alerts.

## MITRE Coverage

Coverage of ATT&CK techniques.

---

# 12 — Deployment Models

## On-Premises

Advantages:

- Data Control
- Regulatory Compliance

Disadvantages:

- High Cost
- Infrastructure Management

## Cloud-Native

Advantages:

- Scalability
- Reduced Maintenance

Examples:

- Sentinel
- Chronicle
- Sumo Logic

## Hybrid

Combines:

- On-Prem Collection
- Cloud Analytics

## MSSP / MDR

Managed Security Services.

Benefits:

- 24/7 Monitoring
- Faster Deployment
- Expert Analysts

---

# SOC Analyst Investigation Workflow

1. Alert Generated
2. Alert Triage
3. Event Correlation
4. IOC Validation
5. Root Cause Analysis
6. Containment
7. Eradication
8. Recovery
9. Lessons Learned

---

# SIEM Best Practices

- Normalize All Data Sources
- Reduce False Positives
- Use Threat Intelligence
- Implement MITRE Mapping
- Maintain Log Retention Policies
- Monitor SIEM Health
- Review Detection Rules Regularly
- Automate Response Where Possible

---

# Conclusion

SIEM is the central nervous system of a Security Operations Center. It collects, stores, analyzes, correlates, and investigates security events across the organization. Modern SIEM platforms integrate with SOAR, Threat Intelligence, UEBA, Cloud Platforms, and MITRE ATT&CK to improve security visibility and accelerate incident response.

---

# Author

**Created By: Mr. Rajan**
Cybersecurity Trainer | SOC Analyst | SIEM Enthusiast
