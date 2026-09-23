#### 🛡️ Lab 9: Host Firewall Configuration with UFW
*Completed on: 15 September 2026*

**Objective:**
Enforce a Default Deny security posture on an Ubuntu host using Uncomplicated Firewall (UFW) and configure granular rules for allowed inbound traffic.

**Commands Run:**
- `sudo ufw status verbose`
- `sudo ufw default deny incoming`
- `sudo ufw default allow outgoing`
- `sudo ufw allow 22/tcp`
- `sudo ufw allow 80/tcp`
- `sudo ufw enable`
- `sudo ufw status numbered`

**What I Observed:**
- **Default Posture:** Established a default-deny baseline blocking all unsolicited incoming traffic while allowing outgoing connections.
- **Rule Table Inspection:** Verified active firewall rules allowing TCP traffic on Port 22 (SSH) and Port 80 (HTTP) for both IPv4 and IPv6 (`22/tcp ALLOW Anywhere`, `80/tcp ALLOW Anywhere`, `22/tcp (v6) ALLOW Anywhere (v6)`, `80/tcp (v6) ALLOW Anywhere (v6)`).
- **Rule Order & IPv6 Support:** Confirmed UFW automatically creates duplicate entries for IPv6 sockets to ensure consistent traffic filtering across protocol stacks.

**Security Relevance:**
Enforcing a default-deny firewall rule set follows the Principle of Least Privilege (PoLP) by dropping unsolicited network probes by default and explicitly restricting open ports to required services, significantly shrinking the host's attack surface.

**Evidence:**
<img width="1261" height="720" alt="image" src="https://github.com/user-attachments/assets/964cc5c9-24e9-49fa-9ea5-561c22322bb0" />
