# MITRE ATT&CK Coverage — Splunk SOC Detection Lab

## Detection Coverage Map

| # | Detection | Tactic | Technique | T-ID | Severity | SPL File |
|---|---|---|---|---|---|---|
| 1 | SSH Brute Force | Credential Access | Brute Force | T1110 | HIGH | ssh_brute_force.spl |
| 2 | Port Scanning | Reconnaissance | Network Service Discovery | T1046 | MEDIUM | port_scan.spl |
| 3 | SQL Injection | Initial Access | Exploit Public-Facing App | T1190 | HIGH | sql_injection.spl |
| 4 | Directory Traversal | Discovery | File & Directory Discovery | T1083 | HIGH | directory_traversal.spl |
| 5 | File Exfiltration | Exfiltration | Exfiltration Over Web | T1041 | MEDIUM | exfiltration.spl |

---

## Coverage by Tactic

| Tactic | Covered | Techniques Detected |
|---|---|---|
| Reconnaissance | ✅ | T1046 |
| Initial Access | ✅ | T1190 |
| Credential Access | ✅ | T1110 |
| Discovery | ✅ | T1083 |
| Exfiltration | ✅ | T1041 |
| Execution | ❌ | Not covered |
| Persistence | ❌ | Not covered |
| Privilege Escalation | ❌ | Not covered |
| Lateral Movement | ❌ | Not covered |

---

## Severity Summary

| Severity | Count | Attacks |
|---|---|---|
| HIGH | 3 | SSH Brute Force, SQL Injection, Directory Traversal |
| MEDIUM | 2 | Port Scan, File Exfiltration |
| LOW | 0 | — |

---

## References

- MITRE ATT&CK Framework : https://attack.mitre.org
- T1110 : https://attack.mitre.org/techniques/T1110
- T1046 : https://attack.mitre.org/techniques/T1046
- T1190 : https://attack.mitre.org/techniques/T1190
- T1083 : https://attack.mitre.org/techniques/T1083
- T1041 : https://attack.mitre.org/techniques/T1041
