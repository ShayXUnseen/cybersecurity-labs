#### 🌐 Lab 7: IP Addressing & Subnetting Audit

*Completed on: 13 September 2026*

**Objective:**
Inspect local network interfaces, analyze IPv4 address structures, determine network/host boundaries using CIDR notation, and verify local gateway routing.

**Commands Run:**
- `ip addr show`
- `ip route show`
- `ping -c 4 10.0.2.2`

**What I Observed:**
- **Local Host IP & CIDR:** Identified interface IP as `10.0.2.15/24`. The `/24` prefix indicates that the first 24 bits (`10.0.2`) represent the network portion, while `.15` is the host ID.
- **Default Gateway:** Identified `10.0.2.2` as the default gateway using `ip route show`.
- **Gateway Connectivity:** Successfully pinged `10.0.2.2` with 0% packet loss, confirming active communication with the local virtual router.

**Security Relevance:**
Understanding IP addressing and subnetting is essential for identifying host locations, mapping local network boundaries, and configuring network segmentation or firewall rules to restrict lateral threat movement.

**Evidence:**
<img width="1303" height="739" alt="Ip address lab 14-09-2026" src="https://github.com/user-attachments/assets/c805bb46-9505-4f7c-af01-9d3c49740a73" />
