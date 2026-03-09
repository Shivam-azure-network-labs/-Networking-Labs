# CCNA Lab 4 – Static Routing with Failover

## Lab Overview
This lab demonstrates Static Routing with a Backup Route (Failover) between multiple branch routers and an ISP router.

The topology contains three branch networks (HR, SALES, IT) connected through routers.  
A primary path and a backup path are configured to ensure connectivity even if the primary link fails.

When the primary link goes down, the backup static route with higher Administrative Distance becomes active.

---

## Topology

![Topology](topology.png)

---

## Network Addressing

| Network | Purpose |
|-------|--------|
| 192.168.10.0/24 | LAN1 – HR |
| 192.168.20.0/24 | LAN2 – SALES |
| 192.168.30.0/24 | LAN3 – IT |
| 10.0.12.0/24 | ISP ↔ R2 |
| 10.0.14.0/24 | ISP ↔ R4 |
| 10.0.24.0/24 | R2 ↔ R3 |
| 10.0.34.0/24 | R3 ↔ R4 |

---

## What I Practiced

- Static Routing configuration
- Default route configuration
- /24 subnet addressing
- End-to-End connectivity testing
- Backup route configuration
- Manual failover simulation

---

## Key Concept

Static routes normally have Administrative Distance = 1.

A **backup route** can be configured by increasing the Administrative Distance.

Example:

ip route 192.168.30.0 255.255.255.0 10.0.24.2 5



The route will only activate if the primary route fails.

---

## Failover Test

Primary link was manually shut down:
interface s0/0/0
shutdown



Routing table verification:

show ip route


Result:

Traffic successfully switched to the backup route and connectivity remained stable.

---

## Devices Used

- Cisco 2911 Router
- Cisco 2960 Switch
- PC-PT
- Cisco Packet Tracer

---


---

## Author

**Shivam Kumar Sinha**

CCNA Networking Labs Series

GitHub:
https://github.com/Shivam-azure-network-labs
