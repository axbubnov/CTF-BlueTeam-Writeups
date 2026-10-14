# Investigating Windows Logs (TryHackMe)

**Scenario:** A suspicious activity was detected on a Windows workstation. The goal is to analyze the exported Event Logs to find traces of compromise.

**Tools Used:** Event Viewer, PowerShell.

## Investigation Steps

1. **Identifying the compromised account:**
   Filtered Security logs by Event ID `4624` (Successful Logon). Noticed a suspicious logon attempt at 2:00 AM for the user `Admin`.

2. **Finding the malicious process:**
   Checked Sysmon logs (Event ID `1` - Process Creation). Found an unusual execution of `powershell.exe -enc <base64_payload>`.
   
3. **Decoding the payload:**
   Decoded the base64 string and discovered an attempt to download a malicious executable from `http://malicious-ip.com/payload.exe`.

## Conclusion
The attacker successfully logged in via RDP (Event ID 4624, Logon Type 10) and executed a PowerShell download cradle to retrieve the second-stage payload.
