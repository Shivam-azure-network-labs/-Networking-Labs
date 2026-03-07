# CCNA Lab 03 – OSPF Multi-Router Topology

## Overview
This lab demonstrates how to configure OSPF (Open Shortest Path First) routing between multiple routers in a network. Three routers are connected using serial links and each router connects to a local LAN network.

The goal of this lab is to allow communication between all LAN networks using OSPF Area 0.

--------------------------------------------------

## Topology

R1 ----- R2 ----- R3

Each router is connected to a switch and two PCs.

LAN Networks:
192.168.10.0/24
192.168.20.0/24
192.168.30.0/24

WAN Networks:
10.10.10.0/30
20.20.20.0/30

--------------------------------------------------

## IP Addressing

Router 1
G0/0  → 192.168.10.1/24
S0/0/0 → 10.10.10.1/30

Router 2
G0/0 → 192.168.20.1/24
S0/0/0 → 10.10.10.2/30
S0/0/1 → 20.20.20.1/30

Router 3
G0/0 → 192.168.30.1/24
S0/0/1 → 20.20.20.2/30

--------------------------------------------------

## OSPF Configuration

OSPF is configured on all routers using Process ID 1 and Area 0.

router ospf 1
network 192.168.10.0 0.0.0.255 area 0
network 192.168.20.0 0.0.0.255 area 0
network 192.168.30.0 0.0.0.255 area 0

--------------------------------------------------

## Verification Commands

show ip route
show ip ospf neighbor
show ip ospf interface
ping <destination-ip>

--------------------------------------------------

## Result

All LAN networks can communicate with each other using OSPF dynamic routing.

Example:
PC0 → PC5 Ping Successful
PC2 → PC4 Ping Successful

--------------------------------------------------

## Skills Practiced

OSPF Configuration  
Multi-Router Routing  
Serial Interface Configuration  
Network Verification  

--------------------------------------------------

Author

Shivam Kumar  
CCNA Networking Labs
