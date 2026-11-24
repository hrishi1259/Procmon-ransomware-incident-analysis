# Response Playbook

## Immediate (0-24 h)
1. Isolate MSEDGEWIN10 and 192.168.1.224; capture memory before power-off (PIDs 7292 and 6020 are live evidence).
2. Block 54.237.236.103 and 192.168.1.224:5895; search DNS, proxy and NetFlow history for both.
3. Disable/reset `helpdesk`; rotate all local administrator passwords and any credential used on the host.
4. Hunt fleet-wide for the wmiexec pattern, `C:\Windows\__<epoch>` files and `*.XqQ8w98UAO`.
5. Check egress logs for any transfer of `de.zip` (~1.03 GB).

## Short term (1-14 days)
1. Rebuild host from a known-good image; restore `C:\CriticalData` from verified backups or shadow copies.
2. Confirm Defender real-time protection and Tamper Protection are enabled fleet-wide.
3. Determine how 192.168.1.224 was compromised and how the helpdesk credential was obtained.
4. Review browser and proxy logs for origin of AnyDesk and the IObit installer.
5. Hash and sandbox the implant, ransomware, LaZagne build and `down.ps1`; assess breach-notification duties.

## Long term
1. LAPS / unique local admin passwords; deny network logon for local accounts.
2. Block inbound SMB, DCOM and WMI between workstations.
3. Enable PowerShell script-block logging and Sysmon; deploy the detections in `/detections`.
4. Application control, offline immutable backups, egress filtering.
