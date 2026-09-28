## 📡 Lab 15: Splunk Universal Forwarder Setup
*Completed on: 28 September 2026*

**Objective:**
Get my Windows VM sending its logs to Splunk live, instead of uploading exported files by hand. This is how a real SOC collects logs from endpoints.

**Background:**
My first attempt was exporting the Security log from Event Viewer as XML and uploading it to Splunk. It worked, but Splunk lumped hundreds of log entries into giant single events, so I couldn't search them properly. A Universal Forwarder streams events one at a time, already separated.

**Actions:**
- Added a second network adapter (Host-only) to both VMs so they could reach each other
- Confirmed the Ubuntu VM had an IP on that network
- Opened receiving port 9997 in Splunk (Settings > Forwarding and receiving)
- Tested the connection from Windows with `Test-NetConnection` on port 9997
- Installed the Splunk Universal Forwarder on the Windows VM and pointed it at Splunk
- Told the forwarder which logs to read (Security, System, Application) in `inputs.conf`

**Troubleshooting:**
- No data showed up in Splunk after the install
- I checked the forwarder's config file (`outputs.conf`) and found a typo in the destination IP: 192.165.56.102 instead of 192.168.56.102
- The network test had passed earlier because I typed the correct IP there, so the network was never the problem
- After fixing the IP and restarting the forwarder service, its log showed a successful connection to Splunk
- The forwarder's own heartbeat logs were visible in Splunk before my Windows events were, which showed the connection worked and I still needed to configure which logs it read

**Findings:**
- Windows events now arrive in Splunk as separate, searchable events with fields like `EventCode`
- I could filter for specific event IDs (for example 4624 for successful logons and 4625 for failed ones) instead of searching raw text

**Security Relevance:**
Getting logs from endpoints into a central SIEM is the foundation of SOC monitoring. Analysts can't investigate what they can't see, so a broken log pipeline is a real problem in an actual SOC. This lab also taught me a habit I'll keep: when data doesn't arrive, check the configuration first, then the network. A single wrong digit in a config file caused the whole issue.

**Evidence:**
<img width="1920" height="996" alt="image" src="https://github.com/user-attachments/assets/e733e900-e0d2-4de1-ba39-befd7a7440fc" />
