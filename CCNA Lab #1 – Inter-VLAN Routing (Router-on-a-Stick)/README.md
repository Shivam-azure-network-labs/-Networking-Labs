# CCNA Lab 01 – Inter-VLAN Routing (Router-on-a-Stick)

## 📌 Objective

The objective of this lab is to configure **Inter-VLAN Routing using the Router-on-a-Stick method** so that devices in different VLANs can communicate with each other through a router.

---

## 🖥️ Network Topology

![Topology](topology.png)
<img width="798" height="626" alt="Screenshot 2026-02-09 121644" src="https://github.com/user-attachments/assets/f7f3713f-7859-482f-8397-0d821f6d75e4" />
[Configuration.txt](https://github.com/user-attachments/files/25811674/Configuration.txt)

This topology contains:

* **1 Router (Cisco 1941)**
* **1 Switch (Cisco 2960)**
* **3 PCs**
* **3 VLANs**

The router is connected to the switch using a **trunk link**, and router **sub-interfaces** are used to route traffic between VLANs.

---

## 🌐 VLAN and IP Addressing

| VLAN   | Network     | Device | IP Address | Default Gateway |
| ------ | ----------- | ------ | ---------- | --------------- |
| VLAN10 | 10.0.1.0/24 | PC1    | 10.0.1.2   | 10.0.1.1        |
| VLAN20 | 10.0.2.0/24 | PC2    | 10.0.2.2   | 10.0.2.1        |
| VLAN30 | 10.0.3.0/24 | PC3    | 10.0.3.2   | 10.0.3.1        |

---

# ⚙️ Switch Configuration

```
enable
configure terminal

vlan 10
name VLAN10

vlan 20
name VLAN20

vlan 30
name VLAN30

interface fa0/1
switchport mode access
switchport access vlan 10

interface fa0/2
switchport mode access
switchport access vlan 20

interface fa0/3
switchport mode access
switchport access vlan 30

interface g0/1
switchport mode trunk

end
```

---

# ⚙️ Router Configuration (Router-on-a-Stick)

```
enable
configure terminal

interface g0/0
no shutdown

interface g0/0.10
encapsulation dot1Q 10
ip address 10.0.1.1 255.255.255.0

interface g0/0.20
encapsulation dot1Q 20
ip address 10.0.2.1 255.255.255.0

interface g0/0.30
encapsulation dot1Q 30
ip address 10.0.3.1 255.255.255.0

end
```

---

# 🧪 Verification

Commands used to verify configuration:

```
show ip interface brief
show vlan brief
show interfaces trunk
ping
```

Connectivity test example:

```
PC1 (10.0.1.2) → ping → PC2 (10.0.2.2)
PC1 (10.0.1.2) → ping → PC3 (10.0.3.2)
```

Successful ping responses confirm that **Inter-VLAN Routing is working correctly**.

---

# 📂 Project Structure

```
Lab-01-Inter-VLAN-Routing
│
├── README.md
├── configuration.txt
└── topology.png
```

---

# 🎯 Conclusion

In this lab, **Inter-VLAN Routing was implemented using Router-on-a-Stick**.
The router was configured with **multiple sub-interfaces and 802.1Q encapsulation** to route traffic between VLANs.

This lab demonstrates how routers can enable communication between different VLANs in a network.

---

# 🚀 Skills Practiced

* VLAN Configuration
* Access Port Configuration
* Trunk Configuration
* Router Sub-Interfaces
* Inter-VLAN Routing
* Basic Network Verification Commands

---

💡 Practicing real-world networking labs daily to strengthen routing and switching fundamentals.

**Consistency beats talent.**
