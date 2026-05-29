# Security Operations Center — Complete Notes

## 01 — DEFINITION
### What is a SOC?

## Security Operations Center [CORE CONCEPT]

A SOC (Security Operations Center) is a centralized, dedicated facility operated by a specialized security team that continuously monitors an organization's network and all its resources to identify suspicious activity and prevent damage. This team operates 24/7/365 — never sleeping, never stopping.

Modern-day threats target digital assets — confidential data stored in networks and systems. Threat actors discover and exploit new vulnerabilities daily. Traditional security alone is not enough, which is why a dedicated SOC team is essential.

### What Does the SOC Protect?

- **Network** — all traffic and communications
- **Systems & Servers** — operating systems, databases, endpoints
- **Applications** — web apps, internal software
- **Data** — confidential records, credentials, secrets

---

## 02 — IMPORTANCE
### Why is SOC Important?

### Industries That Need SOC

- **Banks** — financial data
- **Hospitals** — patient records
- **Government** — national security
- **IT Companies** — intellectual property

### Impact of Compromise

- Data Breaches
- Financial Loss
- Reputation Damage
- Business Disruption

---

## 03 — CORE MISSION
### Detection & Response

The main focus of the SOC is keeping Detection and Response intact, using security solutions that integrate across the entire company's network for centralized monitoring.

### 4 Types of Detection

#### Vulnerability Detection
Identifying weaknesses in software or systems before attackers do — e.g. unpatched Windows systems.

#### Unauthorized Activity
Spotting stolen credentials in use — e.g. login from an unusual geographic location.

#### Policy Violations
Detecting rule breaches — e.g. downloading pirated media or sending company files insecurely.

#### Intrusions
Catching unauthorized access — e.g. attacker exploiting a web application or user visiting a malicious site.

### 3 Main Responsibilities

- **Threat Detection** — Identifying suspicious or malicious activity: failed logins, suspicious IPs, malware signals.
- **Attack Analysis** — Investigating the source, affected systems, attack type, and organizational impact.
- **Incident Response** — Taking action: blocking malicious IPs, isolating infected systems, removing malware, restoring systems.

---

## 04 — FOUNDATION
### 3 Pillars of a Mature SOC

A SOC team matures and efficiently detects/responds to incidents only when all three pillars — People, Process, and Technology — work together.

### People
Skilled analysts (L1, L2, L3) who monitor, investigate, and respond to threats. The human element is irreplaceable.

### Process
Defined workflows and procedures for triage, escalation, and incident response that ensure consistent action.

### Technology
SIEM platforms, firewalls, and detection tools that collect, analyze, and alert on security events.

---

## 05 — TEAM STRUCTURE
### SOC Analyst Tiers

## TIER 1 · FIRST LINE OF DEFENSE
### SOC L1 Analyst

The first responders to alerts. They review incoming security events, perform initial triage, and escalate confirmed threats upward.

- Monitor and review SIEM alerts
- Review logs and events
- Distinguish real threats from false positives
- Escalate serious alerts to L2

**Example:**  
SIEM generates an alert for multiple failed login attempts → L1 analyst reviews it first to confirm if it's a real brute-force attempt or a false alarm.

---

## TIER 2 · DEEP INVESTIGATION
### SOC L2 Analyst

Handles escalated alerts. Goes deeper into the investigation — finding root causes and applying containment measures.

- Investigate escalated alerts in detail
- Identify the root cause of incidents
- Contain and mitigate active threats
- Provide remediation recommendations

**Example:**  
Brute-force attack detected → L2 analyst traces attacker IP addresses and applies firewall rules to block them.

---

## TIER 3 · EXPERT THREAT HUNTERS
### SOC L3 Analyst

Senior security experts who handle complex, advanced threats and proactively hunt for hidden attackers before alerts fire.

- Perform proactive threat hunting
- Handle complex and novel incidents
- Develop new detection rules and signatures
- Improve tools, strategies, and playbooks

**Example:**  
New malware variant appears → L3 analyst studies its behavior, reverse-engineers it, and creates detection rules to catch future infections.

---

## 06 — TECHNOLOGY
### SOC Tools & SIEM

## What is SIEM? [KEY TOOL]

SIEM (Security Information and Event Management) is the central platform of any SOC. It collects logs from all systems, correlates events, detects suspicious patterns, and generates alerts for analysts to investigate.

### Common SOC Tools

- **Splunk** — Industry-leading SIEM for log analysis & dashboards
- **IBM QRadar** — Enterprise SIEM with advanced threat intelligence
- **Firewalls** — Network boundary defense, log source
- **Endpoint Tools (EDR/AV)** — host-level threat detection

### What SIEM Does

- **Log Collection** — Gathers logs from firewalls, servers, endpoints, network devices
- **Log Storage & Correlation** — Stores and correlates events across all sources
- **Pattern Detection** — Automatically detects anomalies and suspicious patterns
- **Alert Generation** — Fires alerts for failed logins, malware activity, suspicious IPs

---

## 07 — WORKFLOW
### SOC Workflow: Logs → Resolution

### 01 Log Generation
Every activity across systems produces logs — user logins, file access, network connections, application events.

### 02 Log Ingestion into SIEM
All logs are collected and ingested into the SIEM platform (e.g. Splunk). The SIEM stores, normalizes, and analyzes all events from a centralized location.

### 03 Alert Generation
When the SIEM detects suspicious patterns it fires an alert — multiple failed logins, suspicious IP activity, malware signatures, policy violations.

### 04 L1 Analyst Investigation
The L1 analyst reviews the alert to determine if it is a genuine threat or a false positive. Initial triage happens here.

### 05 L2 Analyst Deep Analysis
If confirmed serious, the alert is escalated to L2 for deeper investigation — root cause analysis, attacker profiling, impact assessment.

### 06 Incident Response
Attack confirmed → SOC takes action:

- Isolate compromised systems
- Block malicious IPs
- Remove malware
- Recover affected data
- Restore normal operations

---

# Security Operations Center — Complete Notes
### Made by Rajan Behera
