## 🌐 Lab 5: Network Interface & Connectivity Audit
*Completed on: 10 September 2026*

**Objective:**
Identify active network adapters, verify local loopback functionality, test external internet routing, and audit DNS resolution.

**Commands Run:**
- `ip a`
- `ping -c 4 127.0.0.1`
- `ping -c 4 8.8.8.8`
- `nslookup google.com`

**What I Observed:**
- Running `ip a` identified my primary network interface and my assigned private IP address.
- Pinging `127.0.0.1` confirmed that my system's internal TCP/IP network stack is healthy.
- Pinging `8.8.8.8` resulted in 0% packet loss, confirming my default gateway and NAT router are forwarding outbound traffic.
- `nslookup google.com` successfully queried DNS servers to translate the human-readable domain into its public destination IP address.

**Security Relevance:**
When performing incident response or host investigation, inspecting network interfaces helps determine if an infected system is actively connected to the network, isolated, or communicating with external IP addresses.

**Evidence:**
<img width="1292" height="508" alt="image" src="https://github.com/user-attachments/assets/e3807f83-3e5a-4f1c-967d-a59ad748f181" />
<img width="1287" height="394" alt="image" src="https://github.com/user-attachments/assets/f45ff4d6-8494-4cd8-a8ec-e83ef5acd10c" />
