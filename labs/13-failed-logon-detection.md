## 🚨 Lab 13: Failed Logon Detection (Event ID 4625)
*Completed on: 24 September 2026*

**Objective:**
Simulate a failed login scenario in my Windows VM and learn to identify brute-force 
style patterns in Security logs using Event ID 4625.

**Actions:**
- Locked the session and deliberately entered the wrong password several times
- Logged in correctly afterward
- Opened Event Viewer > Security log and located the 4625 (Failed Logon) entries
- Used Filter Current Log to isolate just Event ID 4625, cutting out unrelated noise
- Reviewed the Failure Reason, Account Name, and Logon Type fields on each entry

**Findings:**
- Each failed attempt generated its own 4625 event, with Logon Type 2 (interactive), 
  confirming the attempts happened at the actual login screen rather than remotely
- The Failure Reason field clearly flagged the bad password attempts
- The timestamps across the failed attempts were seconds apart — this is the exact 
  pattern that separates a human mistyping a password from an automated brute-force 
  attempt, which is the real signal a SOC analyst looks for

**Security Relevance:**
4625 is one of the most watched event IDs in real SOC monitoring — a cluster of 
these in a short window, especially against the same account or from the same 
source, is a textbook brute-force indicator. Learning to filter noise and isolate 
just this event ID is the same workflow used in a real SIEM when triaging 
authentication-based alerts.

**Evidence:**

<img width="619" height="604" alt="image" src="https://github.com/user-attachments/assets/d85c2155-3ea5-4bc6-87e3-e29d95405606" />
