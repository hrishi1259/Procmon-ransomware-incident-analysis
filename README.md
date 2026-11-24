# Procmon Ransomware Incident Analysis: MSEDGEWIN10

Incident analysis of a Process Monitor (Procmon) capture from a compromised Windows 10 host. The capture shows a hands-on-keyboard intrusion that moved from reconnaissance to credential theft, ransomware encryption and data staging in under 10 minutes.

> **Severity:** Critical | **Host:** MSEDGEWIN10 (192.168.1.21) | **Capture:** 05:18:10 - 05:32:39 UTC, 03 Nov 2023 | **Events:** 1,432,511

## Summary

| Item | Detail |
|---|---|
| Attacker host | 192.168.1.224 (internal pivot) |
| Initial access (observed) | Abused local `helpdesk` account over SMB (445) and DCOM/WMI (135) |
| Execution | Impacket `wmiexec` pattern via `wmiprvse.exe` (28 commands) |
| Defense evasion | `Set-MpPreference -DisableRealtimeMonitoring 1`, `powershell -ep bypass`, `certutil` |
| Credential access | `reg save` of SAM/SYSTEM, LaZagne (`br0298.exe`) |
| C2 | 192.168.1.224:5895 (implant `SJi8hednh12.exe`) |
| Staging server | 54.237.236.103:443 (plain HTTP on 443) |
| Impact | 58 files in `C:\CriticalData` encrypted (`.XqQ8w98UAO`), ~1.03 GB archived to `de.zip` |

## Repository structure

```
.
├── README.md
├── report/        Full incident report (PDF)
├── docs/          Timeline and MITRE ATT&CK mapping
├── iocs/          Indicators of compromise (CSV)
├── detections/    Sigma rules and Splunk searches
└── response/      Containment and remediation playbook
```

## Key takeaways

- Attack chain: remote access, recon, defense evasion, credential theft, tool drop and C2, LaZagne, ransomware, staging.
- No phishing artefacts were found; the likely vector is stolen or reused helpdesk credentials.
- No shadow-copy deletion was observed, so local recovery should be checked first.
- Persistence could not be confirmed because registry events were not captured.

## Tools and data sources

Procmon (PML capture): process, file system and network event classes. Detection content targets Sysmon / Windows event logs and works in Splunk or any Sigma-compatible SIEM.

## Limitations

Procmon captured no registry events, file hashes, ransom-note content or authentication logs. Ransomware family attribution is not possible from this data.

## Disclaimer

For educational and defensive purposes only. IOCs come from a lab or incident capture and should be validated before production blocking.
