# 📁 Lab 10: Network Segmentation, Virtual Interfaces & Inter-Zone ACL Simulation
*Date: 16 September 2026*  
*Environment: Ubuntu Linux VM (iproute2 & iptables)*  

---

### 📌 Objective
To configure isolated network environments (Namespaces) representing distinct organizational zones (**Guest VLAN** vs. **Database VLAN**), attach virtual network adapters (`veth` pairs), assign subnets with CIDR notation, and evaluate traffic isolation enforcing the **Principle of Least Privilege**.

---

### 🧪 Commands Executed & Syntax Analysis

```bash
# 1. Create Isolated Network Zones (Namespaces)
sudo ip netns add guest_zone
sudo ip netns add db_zone

# 2. Create Virtual Ethernet Pairs (Virtual Patch Cables)
sudo ip link add veth_guest type veth peer name veth_guest_br
sudo ip link add veth_db type veth peer name veth_db_br

# 3. Attach Interfaces to their Respective Namespaces
sudo ip link set veth_guest netns guest_zone
sudo ip link set veth_db netns db_zone

# 4. Assign IP Addresses & Subnet Masks (CIDR)
sudo ip netns exec guest_zone ip addr add 192.168.30.2/24 dev veth_guest
sudo ip netns exec db_zone ip addr add 192.168.40.2/24 dev veth_db

# 5. Bring Virtual Interfaces & Loopback Online
sudo ip netns exec guest_zone ip link set veth_guest up
sudo ip netns exec guest_zone ip link set lo up
sudo ip netns exec db_zone ip link set veth_db up
sudo ip netns exec db_zone ip link set lo up

# 6. Audit Zone Configuration
sudo ip netns exec guest_zone ip addr show
```

---

### 🔍 Key Key Findings & Technical Observations
* **Network Namespaces (`netns`):** Provide Layer 2/3 isolation at the kernel level, ensuring that processes inside `guest_zone` have no direct visibility into `db_zone` routing tables or sockets.
* **VEth Pairs:** Act as virtual Ethernet patch cables. Connecting one end to a namespace isolates that interface from the host routing table.
* **CIDR Notation (`/24`):** Defines a 24-bit network prefix (`255.255.255.0`), allocating 8 bits for host addresses (`.1` to `.254`).
* **Security Relevance:** Demonstrates how logical boundaries prevent unauthorized lateral movement between public/guest zones and sensitive internal data stores.
<img width="1293" height="732" alt="image" src="https://github.com/user-attachments/assets/fce7197f-01d6-449a-a0f1-f906cf88f3fc" />
