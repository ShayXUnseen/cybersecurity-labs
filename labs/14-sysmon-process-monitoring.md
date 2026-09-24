## 🔍 Lab 14: Sysmon Installation & Process Creation Monitoring
*Completed on: 24 September 2026*

**Objective:**
Install Sysmon on my Windows VM to get deeper endpoint visibility than default 
Windows logging provides, and learn to read process creation events.

**Actions:**
- Downloaded Sysmon from Microsoft's official Sysinternals page
- Used the SwiftOnSecurity community config file instead of Sysmon defaults, for 
  a more useful out-of-the-box ruleset
- Installed via: `sysmon64.exe -i sysmonconfig-export.xml`
- Verified logging under Applications and Services Logs > Microsoft > Windows > 
  Sysmon > Operational
- Opened Notepad and located the matching Event ID 1 (Process Creation) entry

**Findings:**
- Sysmon logs every process launch system-wide, not just user-initiated ones — 
  background Windows processes (svchost.exe, RuntimeBroker.exe, etc.) generate 
  their own Event ID 1 entries constantly
- Checked the ParentImage field on the Notepad event and confirmed it was 
  explorer.exe — meaning Notepad was launched normally, from the desktop/Start 
  menu, by Windows Explorer as expected

**Security Relevance:**
The ParentImage field is what makes Sysmon genuinely useful for detection, not 
just logging. A normal process chain (explorer.exe -> notepad.exe) is what 
"healthy" looks like. A suspicious one — like winword.exe spawning 
powershell.exe as a child process — is a well-known indicator of malicious macro 
execution. Learning to read parent-child process relationships is a core skill 
for spotting living-off-the-land attacks, where attackers abuse legitimate 
Windows tools instead of dropping obvious malware.

**Evidence:**

<img width="984" height="700" alt="image" src="https://github.com/user-attachments/assets/f0d3199c-6b61-4e6c-b58d-2a6a329e263f" />
