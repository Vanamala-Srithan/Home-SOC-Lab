# Home SOC Lab

A hands-on **Security Operations Center (SOC) Lab** built using **Wazuh SIEM**, **Ubuntu Server**, and **Kali Linux** to simulate cyber attacks, monitor security events, investigate alerts, and develop practical SOC analyst skills.

---

# Project Objectives

* Deploy a Wazuh SIEM environment
* Monitor Linux endpoints
* Simulate real-world cyber attacks
* Investigate security alerts
* Document incidents using SOC reporting practices
* Map detections to the MITRE ATT&CK Framework
* Develop custom detection rules

---

# Lab Architecture

Host Machine


↓

VirtualBox


↓

Ubuntu Server
(Wazuh Manager)


↓

Kali Linux
(Attacker Machine)


```text
                     Windows 11 Host
                           │
                    Oracle VirtualBox
                           │
        ┌──────────────────┴──────────────────┐
        │                                     │
 Ubuntu Server                         Kali Linux
 (Wazuh Manager)                   (Attacker Machine)
 192.168.29.50                      192.168.29.251
```

---

# Technology Stack

| Component               | Purpose                    |
| ----------------------- | -------------------------- |
| Ubuntu Server 24.04 LTS | Wazuh Manager              |
| Wazuh 4.12              | SIEM Platform              |
| Kali Linux              | Attack Simulation          |
| OpenSSH                 | Authentication Monitoring  |
| Hydra                   | SSH Brute Force Simulation |
| Oracle VirtualBox       | Virtualization             |

---

# Repository Structure

```text
Home-SOC-Lab/
│
├── attacks/
├── reports/
├── screenshots/
├── setup/
├── README.md
└── roadmap.md
```

---

# Completed Attack Simulations

| Attack          | Status | Documentation             |
| --------------- | :----: | ------------------------- |
| SSH Brute Force |    ✅   | attacks/ssh-bruteforce.md |

---

# Incident Reports

| Incident ID | Description                  | Status |
| ----------- | ---------------------------- | :----: |
| HOMESOC-001 | Wazuh Dashboard Inaccessible |    ✅   |
| HOMESOC-002 | SSH Brute Force Detection    |    ✅   |

<<<<<<< HEAD
### Step 3

Access Dashboard

https://192.168.29.50



### Step 4

Register Agent



### Step 5

Generate Events

=======
---
>>>>>>> 1ef4376 (docs: add SSH brute force documentation and incident reports)

# Skills Demonstrated

* SIEM Administration
* Wazuh Deployment
* Linux Administration
* VirtualBox Networking
* SSH Authentication Monitoring
* Threat Hunting
* Log Analysis
* Incident Investigation
* Root Cause Analysis
* MITRE ATT&CK Mapping
* Security Documentation

---

# Detection Scenarios

### Completed

* SSH Authentication Monitoring
* SSH Brute Force Detection
* Wazuh Agent Monitoring

### Planned

* Nmap Scan Detection
* Reverse Shell Detection
* File Integrity Monitoring
* Malware Simulation
* Persistence Detection

---

# Roadmap

## Phase 1 – Lab Deployment ✅

* Ubuntu Server Installation
* Wazuh Installation
* Dashboard Configuration
* Kali Agent Enrollment

## Phase 2 – Attack Simulation ✅

* SSH Brute Force
* Threat Hunting
* Incident Documentation

## Phase 3 – Detection Engineering ⏳

* Custom Wazuh Rules
* Sigma Rules
* MITRE ATT&CK Enrichment

## Phase 4 – Advanced Monitoring ⏳

* Windows Endpoint
* Sysmon Integration
* Suricata Integration
* Threat Intelligence

---

# Screenshots

Screenshots for attack simulations and investigations are available in the **screenshots/** directory.

---

# Disclaimer

This project was developed in an isolated virtual lab environment for educational and defensive cybersecurity purposes. All attack simulations were performed only against systems owned and controlled by the author.

---

# Author

**Srithan Vanamala**

Aspiring SOC Analyst | Cybersecurity Enthusiast
