# MITRE ATT&CK Mapping

| Technique | Name | Evidence |
|---|---|---|
| T1078.003 | Valid Accounts: Local Accounts | Commands run as `MSEDGEWIN10\helpdesk` |
| T1047 | Windows Management Instrumentation | `wmiprvse.exe` spawning `cmd.exe /Q /c` |
| T1021.002 | SMB/Windows Admin Shares | ADMIN$ output files, C$ drops |
| T1570 | Lateral Tool Transfer | `passed.exe`, `SJi8hednh12.exe` written via SMB |
| T1059.001 / T1059.003 | PowerShell / Windows Command Shell | `-ep bypass`, cmd chains |
| T1105 | Ingress Tool Transfer | `certutil -urlcache`, PowerShell download from 54.237.236.103 |
| T1562.001 | Impair Defenses: Disable or Modify Tools | `Set-MpPreference -DisableRealtimeMonitoring 1` |
| T1003.002 | OS Credential Dumping: SAM | `reg save hklm\sam` / `hklm\system` |
| T1555 | Credentials from Password Stores | LaZagne, `vaultcli.dll` |
| T1486 | Data Encrypted for Impact | `passed.exe`, `*.XqQ8w98UAO`, `readme.txt` |
| T1560.001 / T1074.001 | Archive via Utility / Local Data Staging | `tar` to `de.zip` |
| T1070.004 | File Deletion | `Del C:\passed.exe /F /Q` |
| T1571 | Non-Standard Port | C2 on 5895 |
| T1082, T1033, T1016, T1049, T1069, T1135, T1518.001 | Discovery | whoami, ipconfig, net, netstat, wmic AV |
