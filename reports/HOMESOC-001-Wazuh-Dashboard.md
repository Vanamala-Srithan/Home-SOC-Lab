# HOMESOC-001 – Wazuh Dashboard Inaccessible

## Incident Summary

| Field           | Details                                        |
| --------------- | ---------------------------------------------- |
| **Incident ID** | HOMESOC-001                                    |
| **Title**       | Wazuh Dashboard Inaccessible from Windows Host |
| **Date**        | 20 June 2026                                   |
| **Severity**    | Medium                                         |
| **Category**    | Service Availability                           |
| **Status**      | Resolved                                       |

---

# Executive Summary

While deploying the Home SOC Lab, the Wazuh Dashboard was inaccessible from the Windows host machine using a web browser. Although the Wazuh services were running correctly on the Ubuntu Server, remote access over HTTPS failed.

A structured troubleshooting process was performed to verify service availability, network connectivity, firewall configuration, and VirtualBox networking. The investigation identified the Ubuntu firewall (`ufw`) as the root cause. TCP port **443 (HTTPS)** was blocked, preventing remote access to the Wazuh Dashboard.

After allowing inbound HTTPS traffic through the firewall, the dashboard became accessible from the host machine.

---

# Environment

| Component               | Details                 |
| ----------------------- | ----------------------- |
| Host Operating System   | Windows 11              |
| Hypervisor              | Oracle VirtualBox       |
| SIEM Platform           | Wazuh 4.12              |
| Server Operating System | Ubuntu Server 24.04 LTS |
| Service                 | Wazuh Dashboard         |

---

# Affected Asset

| Asset      | Details                 |
| ---------- | ----------------------- |
| Hostname   | Wazuh-Server            |
| IP Address | 192.168.29.50           |
| Service    | Wazuh Dashboard (HTTPS) |

---

# Symptoms Observed

The following symptoms were observed during the investigation:

* Browser displayed **"This site can't be reached."**
* Dashboard could not be accessed remotely.
* Wazuh Dashboard service appeared to be running.
* No response was received from the Windows host over HTTPS.

---

# Investigation Timeline

| Time                  | Activity                                          |
| --------------------- | ------------------------------------------------- |
| Initial Setup         | Wazuh Dashboard deployed successfully             |
| Investigation Started | Remote dashboard access failed                    |
| Step 1                | Verified `wazuh-dashboard` service status         |
| Step 2                | Checked local HTTPS connectivity using `curl`     |
| Step 3                | Verified VirtualBox network configuration         |
| Step 4                | Reviewed Ubuntu firewall rules                    |
| Resolution            | Allowed TCP port 443 through `ufw`                |
| Validation            | Dashboard successfully accessed from Windows host |

---

# Investigation Process

## Step 1 – Verify Dashboard Service

Confirmed that the Wazuh Dashboard service was running successfully.

```bash
sudo systemctl status wazuh-dashboard
```

The service status indicated that the dashboard was active.

---

## Step 2 – Verify Local HTTPS Service

Tested HTTPS connectivity directly on the Ubuntu Server.

```bash
curl -vk https://127.0.0.1
```

The command returned a successful HTTPS response, confirming that the dashboard service was operational.

---

## Step 3 – Verify VirtualBox Networking

Reviewed the VirtualBox network adapter configuration.

Confirmed:

* Virtual machine was connected to the correct network.
* Ubuntu Server had a valid IP address.
* Network communication between host and guest was functioning correctly.

---

## Step 4 – Review Firewall Configuration

Inspection of Ubuntu firewall rules revealed that inbound HTTPS traffic on TCP port **443** was blocked.

---

# Root Cause

The Ubuntu firewall (`ufw`) was blocking inbound HTTPS traffic required for remote access to the Wazuh Dashboard.

Although the dashboard service was functioning correctly, firewall restrictions prevented connections from the Windows host.

---

# Resolution

Allowed inbound HTTPS traffic through the firewall.

```bash
sudo ufw allow 443/tcp
sudo ufw reload
```

---

# Validation

After updating the firewall rules:

* Wazuh Dashboard loaded successfully in the web browser.
* HTTPS connectivity was verified.
* Login page became accessible.
* Normal dashboard functionality was restored.

---

# Impact Assessment

| Category        | Assessment                                                       |
| --------------- | ---------------------------------------------------------------- |
| Confidentiality | No impact                                                        |
| Integrity       | No impact                                                        |
| Availability    | Dashboard unavailable until firewall configuration was corrected |

---

# Evidence

Include screenshots demonstrating:

* Wazuh Dashboard inaccessible before remediation
* `systemctl status wazuh-dashboard`
* Local HTTPS verification using `curl`
* Firewall rule modification
* Successful Wazuh Dashboard login page after resolution

---

# Lessons Learned

* Always verify local service availability before investigating network connectivity.
* Firewall configuration should be validated whenever a service is reachable locally but inaccessible remotely.
* VirtualBox networking should be confirmed during initial lab deployment.
* Systematic troubleshooting reduces unnecessary configuration changes and helps identify the true root cause more efficiently.

---

# Recommendations

* Verify firewall rules immediately after deploying network services.
* Document required ports for all Home SOC components.
* Validate connectivity after every major configuration change.
* Maintain an incident log for future troubleshooting and knowledge sharing.

---

# Skills Demonstrated

* Linux System Administration
* Ubuntu Firewall (`ufw`) Management
* Service Troubleshooting
* Network Connectivity Analysis
* VirtualBox Networking
* Wazuh Administration
* Root Cause Analysis
* Incident Documentation

---

# Incident Status

**Status:** ✅ Closed

The Wazuh Dashboard was successfully restored and remained accessible after updating the firewall configuration.
