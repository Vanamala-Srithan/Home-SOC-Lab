# HOMESOC-002 – SSH Brute Force Attack Detection

## Incident Summary

| Field            | Details                                    |
| ---------------- | ------------------------------------------ |
| **Incident ID**  | HOMESOC-002                                |
| **Title**        | SSH Brute Force Attack Detection           |
| **Date**         | 21 June 2026                               |
| **Severity**     | Medium                                     |
| **Category**     | Credential Access                          |
| **MITRE ATT&CK** | T1110.001 – Brute Force: Password Guessing |
| **Status**       | Resolved (Lab Exercise)                    |

---

# Executive Summary

A simulated SSH brute-force attack was conducted from a Kali Linux virtual machine against the Ubuntu Server hosting the Wazuh SIEM platform. The objective was to evaluate Wazuh's ability to detect repeated authentication failures and successful logins.

The attack was performed using Hydra against a test account (`socuser`). Wazuh successfully ingested authentication logs, generated alerts for failed and successful login attempts, and provided sufficient information to investigate the activity.

This exercise demonstrates the complete Security Operations Center (SOC) workflow:

**Attack → Detection → Investigation → Documentation**

---

# Environment

| Component      | Details                 |
| -------------- | ----------------------- |
| Host OS        | Windows 11              |
| Hypervisor     | Oracle VirtualBox       |
| SIEM           | Wazuh 4.12              |
| Server         | Ubuntu Server 24.04 LTS |
| Attacker       | Kali Linux              |
| Attack Tool    | Hydra                   |
| Target Service | OpenSSH                 |

---

# Affected Asset

| Item        | Value         |
| ----------- | ------------- |
| Hostname    | Wazuh-Server  |
| Target IP   | 192.168.29.50 |
| Service     | SSH           |
| Target User | socuser       |

---

# Attack Source

| Item        | Value          |
| ----------- | -------------- |
| Source Host | Kali Linux     |
| Source IP   | 192.168.29.251 |
| Attack Tool | Hydra          |

---

# Attack Scenario

The attacker attempted to gain unauthorized access by repeatedly guessing the password for a valid SSH user account using Hydra.

Attack Command:

```bash
hydra -t 2 -l socuser -P passwords.txt ssh://192.168.29.50
```

The password list contained several candidate passwords, including the correct password configured for the test account.

---

# Investigation Timeline

| Time  | Activity                                   |
| ----- | ------------------------------------------ |
| 09:45 | Verified SSH connectivity                  |
| 09:47 | Hydra attack launched                      |
| 09:48 | Multiple authentication failures detected  |
| 09:49 | Successful SSH authentication recorded     |
| 09:50 | Investigation performed in Wazuh Dashboard |
| 09:55 | Incident documented                        |

---

# Detection

The Wazuh Manager collected authentication logs from the Ubuntu server and generated the following alerts.

| Rule ID | Description                  | Level |
| ------- | ---------------------------- | ----: |
| 5760    | SSH authentication failed    |     5 |
| 5557    | Password verification failed |     5 |
| 5503    | PAM authentication failure   |     5 |
| 5715    | SSH authentication success   |     3 |

---

# Investigation Findings

The alert investigation revealed the following evidence:

### Source IP

```text
192.168.29.251
```

### Target IP

```text
192.168.29.50
```

### Username

```text
socuser
```

### Authentication Result

```text
Accepted password for socuser from 192.168.29.251
```

The authentication logs confirmed that multiple failed login attempts originated from the Kali Linux attacker before a successful login was recorded using valid credentials.

---

# Root Cause

Password-based SSH authentication allowed repeated authentication attempts against a valid user account.

In this controlled laboratory environment, the successful login was intentional and performed as part of the attack simulation.

---

# Impact Assessment

| Category        | Assessment                  |
| --------------- | --------------------------- |
| Confidentiality | No impact (Lab Environment) |
| Integrity       | No impact                   |
| Availability    | No impact                   |

The activity occurred within an isolated Home SOC Lab and posed no risk to production systems.

---

# Evidence

## Evidence 1 – Hydra Execution

The attack originated from the Kali Linux virtual machine using Hydra against the Ubuntu SSH service.

![Hydra Attack](../screenshots/ssh-bruteforce/hydra-attack.png)

---

## Evidence 2 – Authentication Alerts

Wazuh detected multiple SSH authentication events generated during the attack.

![Authentication Alerts](../screenshots/ssh-bruteforce/ssh-authentications.png)

---

## Evidence 3 – Successful Login Investigation

The investigation confirmed:

- Source IP
- Username
- Successful authentication
- SSH daemon log

![Authentication Success Details](../screenshots/ssh-bruteforce/authentication-success-details.png)

---

## Evidence 4 – Validation

SSH access was successfully established after authentication, confirming end-to-end monitoring by Wazuh.

![SSH Access](../screenshots/ssh-bruteforce/ssh-access.png)

---

# Recommendations

* Disable password-based SSH authentication where possible.
* Use SSH public key authentication.
* Enforce strong password policies.
* Disable remote root login.
* Deploy Fail2Ban to block repeated failed login attempts.
* Restrict SSH access using firewall rules or VPN.
* Continuously monitor authentication logs using SIEM.
* Enable Multi-Factor Authentication (MFA) where applicable.

---

# Lessons Learned

This exercise demonstrated how Wazuh can detect Linux authentication events associated with SSH brute-force attacks. Analysts were able to identify the attack source, target account, authentication outcome, and relevant security events using the Wazuh Dashboard.

The investigation reinforced the importance of continuous log monitoring, centralized event correlation, and structured incident documentation within a Security Operations Center.

---

# Skills Demonstrated

* Wazuh SIEM Administration
* Linux Log Analysis
* SSH Authentication Monitoring
* Hydra Brute Force Simulation
* Threat Hunting
* Incident Investigation
* MITRE ATT&CK Mapping
* Security Monitoring
* Incident Documentation

---

# Incident Status

**Status:** ✅ Closed

The attack was successfully detected, investigated, and documented within the Home SOC Lab.
