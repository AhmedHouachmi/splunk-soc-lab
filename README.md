# Splunk SOC Detection Lab

A hands-on Security Operations Center lab built with Splunk Enterprise, simulating real attack scenarios from Kali Linux and detecting them using custom SPL rules mapped to the MITRE ATT&CK framework.

---

## Architecture

```
+------------------+          +------------------+
|   Kali Linux     |  attack  |  Victim Machine  |
|  (Attacker)      | -------> |  Ubuntu 22.04    |
|                  |          |  Apache + SSH     |
|  Hydra           |          |  Splunk UF        |
|  Nmap            |          +--------+---------+
|  sqlmap          |                   |
|  curl            |              logs |
+------------------+                   v
                             +------------------+
                             |  Splunk Server   |
                             |  Ubuntu 22.04    |
                             |  Splunk Enterprise|
                             |  SPL Rules       |
                             |  Alerts          |
                             |  Dashboard       |
                             +------------------+
```

| Machine | OS | RAM | Role |
|---|---|---|---|
| Splunk Server | Ubuntu 22.04 | 3.5 GB | Splunk Enterprise + log collection |
| Victim Machine | Ubuntu 22.04 | 1.5 GB | Universal Forwarder + Apache + SSH |
| Kali Linux | Kali Rolling | 2 GB | Attack simulation |

**Log sources monitored :**
- `/var/log/auth.log` → SSH authentication events
- `/var/log/apache2/access.log` → Web server access events

---

## Attack Scenarios & MITRE ATT&CK Mapping

| # | Attack | Tool | Tactic | Technique | T-ID | Severity |
|---|---|---|---|---|---|---|
| 1 | SSH Brute Force | Hydra | Credential Access | Brute Force | T1110 | HIGH |
| 2 | Port Scanning | Nmap | Reconnaissance | Network Service Discovery | T1046 | MEDIUM |
| 3 | SQL Injection | curl + sqlmap | Initial Access | Exploit Public-Facing App | T1190 | HIGH |
| 4 | Directory Traversal | curl | Discovery | File & Directory Discovery | T1083 | HIGH |
| 5 | File Exfiltration | curl | Exfiltration | Exfiltration Over Web | T1041 | MEDIUM |

---

## Detection Rules

All SPL detection rules are in the `/detection-rules` folder.

| File | Attack Detected |
|---|---|
| `ssh_brute_force.spl` | SSH Brute Force (T1110) |
| `port_scan.spl` | Port Scanning (T1046) |
| `sql_injection.spl` | SQL Injection (T1190) |
| `directory_traversal.spl` | Directory Traversal (T1083) |
| `exfiltration.spl` | File Exfiltration (T1041) |

---

## Automated Alerts

Two scheduled Splunk alerts configured to fire automatically :

| Alert | Trigger Condition | Severity | Schedule |
|---|---|---|---|
| SSH Brute Force Detected | > 5 failed logins from same IP | High | Every 5 min |
| SQL Injection Attempt Detected | SQLi pattern in Apache URI | Critical | Every 5 min |

---

## SOC Dashboard

3-panel SOC operations dashboard built in Splunk :

- **Panel 1 — MITRE ATT&CK Coverage** : All 5 detections mapped to tactics, techniques, T-IDs and severity
- **Panel 2 — Top Attacking IPs** : Bar chart ranking source IPs by total event count
- **Panel 3 — Attack Distribution** : Pie chart showing threat breakdown by attack type

---

## Tools & Technologies

**Detection :** Splunk Enterprise · SPL · Universal Forwarder

**Attack Simulation :** Kali Linux · Hydra · Nmap · sqlmap · curl

**Framework :** MITRE ATT&CK

**Infrastructure :** VMware · Ubuntu 22.04 · Apache2 · OpenSSH · PHP

