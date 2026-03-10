

# CCNA Enterprise Mega Lab

### Hybrid Routing Design (OSPF + Static + Default Route)

## 📌 Project Overview

This project simulates a **small enterprise network architecture** using Cisco Packet Tracer.
The topology contains multiple routers, departmental LANs, VLAN segmentation, and an ISP connection.

The goal of this lab was to implement a **hybrid routing architecture** combining:

* **OSPF dynamic routing** for internal core networks
* **Static routing** for branch networks
* **Default route** for internet connectivity through ISP

This design reflects how real enterprise networks maintain **dynamic adaptability internally while keeping external routing stable**.


---

## Topology

![Topology](topology.png)

---


## 🌐 Network Addressing Plan

### WAN Links

| Link           | Network      |
| -------------- | ------------ |
| HQ ↔ CORE-A    | 10.0.1.0/30  |
| HQ ↔ CORE-B    | 10.0.2.0/30  |
| CORE-A ↔ SALES | 10.0.3.0/30  |
| SALES ↔ HR     | 10.0.4.0/30  |
| SALES ↔ IT     | 10.0.5.0/30  |
| CORE-B ↔ R&D   | 10.0.6.0/30  |
| R&D ↔ FINANCE  | 10.0.7.0/30  |
| R&D ↔ SUPPORT  | 10.0.8.0/30  |
| HQ ↔ ISP       | 200.0.0.0/30 |

---

## 🏢 Department Networks

| Department | Network         | Gateway      |
| ---------- | --------------- | ------------ |
| HR         | 192.168.10.0/24 | 192.168.10.1 |
| SALES      | 192.168.20.0/24 | 192.168.20.1 |
| IT         | 192.168.30.0/24 | 192.168.30.1 |
| FINANCE    | 192.168.40.0/24 | 192.168.40.1 |
| R&D        | 192.168.50.0/24 | 192.168.50.1 |
| SUPPORT    | 192.168.60.0/24 | 192.168.60.1 |

---

## ⚙️ Routing Strategy

### 1️⃣ Internal Core Routing

OSPF is used between:

* HEADQUARTER
* CORE-A
* CORE-B

This allows automatic route learning and scalability.

Example configuration:

```
router ospf 1
 router-id 3.3.3.3
 network 10.0.1.0 0.0.0.3 area 0
 network 10.0.2.0 0.0.0.3 area 0
```

---

### 2️⃣ Branch Routing

Branch routers use **static routes** pointing toward their upstream router.

Example:

```
ip route 0.0.0.0 0.0.0.0 10.0.4.1
```

---

### 3️⃣ Internet Connectivity

The enterprise network connects to an **ISP router**.

HQ router forwards unknown traffic using a **default route**:

```
ip route 0.0.0.0 0.0.0.0 200.0.0.1
```

The default route is then **redistributed into OSPF** so internal routers learn the internet path.

```
default-information originate
```

---

## 🧩 Special Implementation

In some routers the LAN interface module did not allow direct IP addressing.

Solution:

* Created **SVI (Switch Virtual Interface)**
* Assigned IP address to **VLAN interface**
* Used it as **default gateway**

Example:

```
interface vlan10
 ip address 192.168.20.1 255.255.255.0
 no shutdown
```

---

## 🔧 Troubleshooting Performed

During implementation several issues were encountered and resolved:

• OSPF neighbors not forming
• Static route next-hop misconfiguration
• Missing default route toward ISP
• Ping reaching HQ but not ISP
• ARP causing first ping failure
• Interface modules not accepting IP configuration

Verification commands used:

```
show ip route
show ip ospf neighbor
show ip protocols
ping
traceroute
```

---

## ✅ Final Results

✔ Full connectivity between all LAN networks
✔ Internal routing automatically learned via OSPF
✔ Static routes correctly redistributed into OSPF
✔ Default route successfully propagated to all routers
✔ End-to-end connectivity including ISP

---

## 🛠 Tools Used

* Cisco Packet Tracer
* Cisco IOS CLI
* CCNA Routing Concepts

---

## 🎯 Key Learning

This lab demonstrates that networking is not just about CLI commands.
It requires understanding:

* routing logic
* traffic flow
* gateway hierarchy
* structured troubleshooting

---

## 👨‍💻 Author

**Shivam Kumar Sinha**

GitHub
https://github.com/Shivam-azure-network-labs

Part of my **CCNA Networking Labs Series** where I practice real-world networking scenarios.


