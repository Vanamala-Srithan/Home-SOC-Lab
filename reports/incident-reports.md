# Home SOC Incident Reports

---

## HOMESOC-001 – Wazuh Dashboard Inaccessible

**Incident ID:** HOMESOC-001

**Date:** 2026-06-20

### Issue

Unable to access the Wazuh Dashboard from the Windows host machine.

### Investigation

Performed the following troubleshooting steps:

* Verified that the `wazuh-dashboard` service was running.
* Confirmed the HTTPS service was responding locally using:

```bash
curl -vk https://127.0.0.1
```

* Checked VirtualBox network configuration.
* Determined that the Ubuntu firewall (`ufw`) was blocking inbound TCP port 443.

### Resolution

Allowed HTTPS traffic through the firewall and reloaded the rules.

```bash
sudo ufw allow 443/tcp
sudo ufw reload
```

### Root Cause

Inbound HTTPS connections to the Wazuh Dashboard were blocked by the Ubuntu firewall.

### Lessons Learned

* Verify service availability locally before investigating network issues.
* Check firewall rules whenever a service is accessible locally but not remotely.
* Validate VirtualBox networking modes during connectivity troubleshooting.

### Status

✅ Resolved

---
