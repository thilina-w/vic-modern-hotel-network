# Vic Modern Hotel Network Design & Implementation

# Overview

This project designs and implements the network infrastructure for **Vic Modern Hotel**,
a three-floor building housing eight departments across three floors. The network uses
three routers (one per floor, all physically located in the IT server room), OSPF for
dynamic routing, VLAN segmentation per department, DHCP for automatic addressing, and
SSH with switch port security for secure administration.

# Building Layout

| Floor | Departments |
|-------|-------------|
| 1st Floor | Reception, Store, Logistics |
| 2nd Floor | Finance, HR, Sales/Marketing |
| 3rd Floor | IT, Admin |

# Network Design

**Router interconnection (serial DCE, point-to-point):**

| Link | Network |
|------|---------|
| Router 1 ↔ Router 2 | 10.10.10.0/30 |
| Router 2 ↔ Router 3 | 10.10.10.4/30 |
| Router 1 ↔ Router 3 | 10.10.10.8/30 |

**VLAN and IP allocation per department:**

| Floor | Department | VLAN | Network |
|-------|------------|------|---------|
| 1st | Reception | 80 | 192.168.8.0/24 |
| 1st | Store | 70 | 192.168.7.0/24 |
| 1st | Logistics | 60 | 192.168.6.0/24 |
| 2nd | Finance | 50 | 192.168.5.0/24 |
| 2nd | HR | 40 | 192.168.4.0/24 |
| 2nd | Sales/Marketing | 30 | 192.168.3.0/24 |
| 3rd | Admin | 20 | 192.168.2.0/24 |
| 3rd | IT | 10 | 192.168.1.0/24 |

# Requirements Implemented

- [x] Three routers connecting each floor, all placed in the IT server room
- [x] Routers interconnected via serial DCE cables
- [x] One switch per floor
- [x] WiFi access on each floor for laptops and phones
- [x] One printer per department
- [x] Each department in its own VLAN
- [x] OSPF as the dynamic routing protocol
- [x] DHCP services provided by each router for its connected devices
- [x] Full end-to-end connectivity between all devices
- [x] SSH enabled on all routers for remote administration
- [x] Test-PC added to the IT department switch (port Fa0/1) to verify remote login
- [x] Port security on the IT switch (sticky MAC, violation mode: shutdown) restricting
      port Fa0/1 to Test-PC only

# Implementation Stages

1. **Infrastructure Design** — Routers, switches, access points, PCs and printers placed
   and cabled per floor.
2. **VLANs & Inter-VLAN Routing** — Departmental VLANs configured on each switch; inter-VLAN
   routing implemented using the router-on-a-stick method.
3. **Dynamic Addressing** — Each router configured as a DHCP server for its local VLANs.
4. **OSPF Routing** — OSPF configured on all routers to advertise routes and enable
   full network reachability.
5. **SSH Configuration** — SSH enabled on all routers (domain name, RSA keys, local user,
   VTY lines restricted to SSH) for secure remote management.
6. **Port Security** — Sticky MAC address port security configured on the IT switch with
   shutdown violation mode, locking port Fa0/1 to Test-PC.

## Tools

- Cisco Packet Tracer
