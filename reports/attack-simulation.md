# SSH Brute Force Simulation

## Objective

Trigger Wazuh alerts using failed SSH login attempts.

---

## Tool Used

Hydra

---

## Command

```bash
hydra -l root -P rockyou.txt ssh://192.168.29.50
```

---

## Result

Authentication attempts failed.

Wazuh generated alerts.

---

## Screenshot

screenshots/alerts.png