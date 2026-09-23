#### 🔌 Lab 8: Active Ports & Services Audit

*Completed on: 14 September 2026*

**Objective:**
Audit active listening ports, transport protocols (TCP/UDP), and associated system processes using socket inspection utilities.

**Commands Run:**
- `sudo netstat -tunlp`
- `sudo lsof -i`

**What I Observed:**
- **DNS Service (Port 53/TCP):** Identified `systemd-resolved` listening on port 53 to handle local domain name resolution.
- **Printing Daemon (Port 631/TCP & TCP6):** Identified `cupsd` listening on both IPv4 and IPv6 sockets for print management.
- **Transport Sockets:** Verified how transport sockets differentiate between IPv4 (`tcp`) and IPv6 (`tcp6`) bindings.

**Security Relevance:**
Auditing open listening ports helps security analysts map a system's attack surface, verify that only required business services are exposed, and identify unauthorized or unneeded background daemons.

**Evidence:**
<img width="1299" height="736" alt="image" src="https://github.com/user-attachments/assets/c699ebce-c054-4542-a1a2-4d253fc649ec" />
