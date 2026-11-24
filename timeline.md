# Attack Timeline (UTC, 03 Nov 2023)

| Time | Phase | Observation |
|---|---|---|
| 05:18:46 | Remote access | Inbound SMB then DCOM/WMI from 192.168.1.224 as `MSEDGEWIN10\helpdesk`; four wmiexec sessions (28 commands) |
| 05:19:43-05:20:20 | Discovery | `whoami /all`, `ipconfig /all`, `net use/user/share/localgroup`, `netstat -ano`, WMIC AntiVirusProduct query |
| 05:21:05 | Defense evasion | `Set-MpPreference -DisableRealtimeMonitoring 1` |
| 05:21:13-17 | Credential dumping | `reg save hklm\sam` and `hklm\system`, files fetched over SMB |
| 05:21:25-05:22:22 | Target discovery | `cd CriticalData`, repeated `dir` |
| 05:21:56 / 05:22:17 | Tool transfer | `passed.exe` and `SJi8hednh12.exe` written to C$ share |
| 05:22:53 | Execution and C2 | Implant connects to 192.168.1.224:5895; spawns cmd, whoami, `powershell -ep bypass`; second instance 05:26:36 |
| 05:25:08-19 | Ingress tool transfer | PowerShell pulls 11.8 MB from 54.237.236.103:443 to `br0298.exe`; `certutil` fetches `down.ps1` |
| 05:26:04-12 | Possible loader/injection | ~11,275 file events probing `SysWOW64\svchost.exe`, 289 thread creations (medium-low confidence) |
| 05:26:50-57 | Credential harvesting | `br0298.exe` (LaZagne PyInstaller build) run plain and with `browsers` |
| 05:27:31-05:28:41 | Ransomware | `passed.exe` encrypts 58 files to `.XqQ8w98UAO`, drops `C:\readme.txt`, self-deletes via ping delay and `Del` |
| 05:28:52-05:29:26 | Staging | `tar -a -c -f de.zip *.XqQ8w98UAO` creates ~1.03 GB archive |
| 05:32:32 | Still active | Implant still beaconing at end of capture |
