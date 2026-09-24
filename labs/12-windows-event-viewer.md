## 🪟 Lab 12: Windows Event Viewer - Logon Auditing
*Completed on: 24 September 2026*

**Objective:**
Set up a Windows VM alongside my Ubuntu lab and get familiar with Event Viewer, 
specifically the Security log, since this is where most real SOC alerts come from.

**Actions:**
- Opened Event Viewer and navigated to Windows Logs > Security
- Cleared the log, then signed out and signed back in to generate fresh events
- Filtered through the results looking for Event ID 4624 (Logon) and 4634 (Logoff)

**Findings:**
- A single sign-in generated way more than one 4624 event. I counted several 
  Logon Type 2 (interactive) entries within seconds of each other, all clustered 
  around 8:24:15–8:24:19 AM
- Turns out this is normal Windows behavior, not a mistake on my end. One sign-in 
  isn't one event under the hood — the lock screen auth, the session unlock, and 
  background processes tied to my account can each generate their own Logon Type 
  2 entry within the same few seconds
- Total noise after just one sign-in: 39 events. Most of it was background account/
  system checks (4672 Special Logon, 4798 User Account Management, 5058/5059/5061 
  system integrity checks) I never directly triggered
- The actual skill wasn't finding *a* 4624 — it was filtering the noise and 
  matching the entries that mapped to my one real action, using the Account Name 
  field and the timestamp cluster

**Security Relevance:**
This is basically alert correlation in miniature, which is a core SOC skill. Real 
SIEM tools face this exact problem at scale — one action triggers multiple log 
lines, and an analyst has to group them into "this is one event," not treat every 
line as its own incident. Recognizing a cluster of same-type events within a few 
seconds as one action instead of five is the kind of triage judgment a SOC L1 
analyst uses daily.

**Evidence:**
<img width="1362" height="986" alt="image" src="https://github.com/user-attachments/assets/50790dc6-6880-4517-9857-d6baa7b1cf06" />
