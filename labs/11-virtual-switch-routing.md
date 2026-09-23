#### 🌉 Lab 11: Virtual Switch, Layer 3 Routing & Firewall Segmentation
*Completed on: 17 September 2026*

**Objective:**
Construct a central Linux Bridge (`br0`) to act as a virtual Layer 2 switch and Layer 3 gateway router between two isolated subnets (`guest_zone` at `192.168.30.0/24` and `db_zone` at `192.168.40.0/24`). Enable kernel packet forwarding to allow communication, and enforce network access control (Default Deny) using `iptables` firewall rules to block unauthorized lateral movement.

**Commands Run:**
```bash
# 1. Virtual Switch Creation & Activation
sudo ip link add name br0 type bridge
sudo ip link set br0 up

# 2. Interface Cable Pair Setup & Switch Attachment
sudo ip link add veth_guest type veth peer name veth_guest_br
sudo ip link set veth_guest netns guest_zone
sudo ip link set veth_guest_br master br0
sudo ip link set veth_guest_br up
sudo ip netns exec guest_zone ip addr add 192.168.30.2/24 dev veth_guest
sudo ip netns exec guest_zone ip link set veth_guest up

sudo ip link add veth_db type veth peer name veth_db_br
sudo ip link set veth_db netns db_zone
sudo ip link set veth_db_br master br0
sudo ip link set veth_db_br up
sudo ip netns exec db_zone ip addr add 192.168.40.2/24 dev veth_db
sudo ip netns exec db_zone ip link set veth_db up

# 3. Layer 3 Gateway & Routing Configuration
sudo ip addr add 192.168.30.1/24 dev br0
sudo ip addr add 192.168.40.1/24 dev br0
sudo ip netns exec guest_zone ip route add default via 192.168.30.1
sudo ip netns exec db_zone ip route add default via 192.168.40.1
sudo sysctl -w net.ipv4.ip_forward=1

# 4. Initial Routing Verification (Inter-Subnet Ping)
sudo ip netns exec guest_zone ping -c 2 192.168.40.2

# 5. Firewall Rule Enforcement (Inserting Top-Priority DROP Rule)
sudo iptables -I FORWARD 1 -s 192.168.30.0/24 -d 192.168.40.0/24 -j DROP

# 6. Rule Priority & Line Number Audit
sudo iptables -L FORWARD -v -n --line-numbers

# 7. Post-Firewall Connectivity Test
sudo ip netns exec guest_zone ping -c 2 -W 2 192.168.40.2
```

**What I Observed:**
* **Central Switch Setup:** Attaching host-side cable endpoints (`veth_guest_br`, `veth_db_br`) to `br0` created a single Layer 2 switching domain across distinct network namespaces.
* **Routing Activation:** Assigning gateway IPs (`192.168.30.1` and `192.168.40.1`) to `br0` and enabling `net.ipv4.ip_forward=1` transformed the host into a Layer 3 router, allowing `guest_zone` to ping `db_zone` with 0% packet loss.
* **Firewall Rule Ordering:** `iptables` processes rules strictly from top to bottom (first matching rule wins). Inserting the DROP rule at Position 1 (`-I FORWARD 1`) ensured it took precedence over any default or broad permit rules.
* **Firewall Enforcement:** Pinging `192.168.40.2` from `guest_zone` resulted in **100% packet loss**, confirming that traffic was actively intercepted and dropped by the firewall.

**Security Relevance (SOC Analyst Takeaway):**
Unrestricted routing across subnets exposes critical infrastructure to lateral movement. Enforcing the Principle of Least Privilege (PoLP) and Default Deny policies at network boundaries using firewalls/ACLs ensures untrusted zones (e.g., Guest Wi-Fi) cannot reach sensitive internal assets (e.g., core database servers). Furthermore, understanding rule precedence in packet filtering is essential for avoiding accidental security bypasses caused by misordered firewall policies.
<img width="1220" height="671" alt="image" src="https://github.com/user-attachments/assets/4b9af44b-8534-4f8e-b8ab-633f43be1b55" />
<img width="1228" height="763" alt="image" src="https://github.com/user-attachments/assets/a74ce123-fbda-4796-bafe-2ad2b6d4c94c" />
<img width="1220" height="762" alt="image" src="https://github.com/user-attachments/assets/06ef3faf-c2da-462c-ab82-35b2a81b46ec" />
<img width="1213" height="762" alt="image" src="https://github.com/user-attachments/assets/3b12f110-09f9-4556-9fdf-27e55a1662ad" />
