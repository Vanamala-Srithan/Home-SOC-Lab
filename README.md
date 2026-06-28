# Home SOC Lab

## Overview

A Security Operations Center lab built using Wazuh for log analysis, monitoring, and threat detection.

---

# Objectives

- Install Wazuh Server
- Configure Wazuh Dashboard
- Monitor Linux endpoints
- Generate alerts
- Investigate security events


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



---

# Components Used

| Component | Purpose |
|----------|---------|
| Ubuntu Server | Wazuh Manager |
| Wazuh | SIEM Platform |
| Kali Linux | Attack Simulation |
| VirtualBox | Virtualization |


---

# Installation Process


### Step 1

Install Ubuntu Server


### Step 2

Install Wazuh


### Step 3

Access Dashboard

https://192.168.29.50



### Step 4

Register Agent



### Step 5

Generate Events




---

# Detection Scenarios


## Failed SSH Login

Alert generated after multiple failed attempts.


## Brute Force Detection

Wazuh rule triggered.


---

## Custom Rules

Rule ID: 100100

Purpose:
Detect repeated SSH authentication failures.

Severity:
5

---


# Screenshots

See screenshots folder.


---

# Future Enhancements

Suricata Integration

Sysmon Integration

Sigma Rules

Threat Intelligence Feed


---

# Author

Srithan Vanamala
