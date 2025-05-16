# 🌐 Static Routing Lab: Full 2-Router, 4-PC Network

## Scenario

You are a junior network admin tasked with configuring a basic routed network between two small LANs in different buildings. Each LAN uses its own private IP space. Your job is to:
- Assign IPs
- Configure router interfaces
- Set static routes
- Verify full end-to-end connectivity

---

## Objectives

- Configure IP addresses on routers and PCs
- Enable router interfaces
- Use static routes to connect the LANs
- Test connectivity with ping
- View routing and MAC address tables

---

## Topology Overview

- **Router0** connects to LAN1 (192.168.1.0/28)
- **Router1** connects to LAN2 (10.0.0.0/28)
- The routers are connected via a point-to-point link using 192.168.50.0/30

---

## IP Addressing Plan

| Device     | Interface        | IP Address         | Description           |
|------------|------------------|--------------------|------------------------|
| **PC0**    | NIC              | 192.168.1.10       | Left LAN Host         |
| **PC2**    | NIC              | 192.168.1.11       | Left LAN Host         |
| **Router0**| G0/1 (to SW0)    | 192.168.1.1        | Gateway for LAN 1     |
| **Router0**| G0/0 (to R1)     | 192.168.50.1       | P2P to Router1        |
| **Router1**| G0/0 (to R0)     | 192.168.50.2       | P2P to Router0        |
| **Router1**| G0/1 (to SW1)    | 10.0.0.1           | Gateway for LAN 2     |
| **PC1**    | NIC              | 10.0.0.10          | Right LAN Host        |
| **PC3**    | NIC              | 10.0.0.11          | Right LAN Host        |

---

## Router Configuration

### Router0

```bash
enable
configure terminal

interface g0/0
ip address 192.168.50.1 255.255.255.252
no shutdown
exit

interface g0/1
ip address 192.168.1.1 255.255.255.240
no shutdown
exit

ip route 10.0.0.0 255.255.255.240 192.168.50.2
Router1
bash
Copy
Edit
enable
configure terminal

interface g0/0
ip address 192.168.50.2 255.255.255.252
no shutdown
exit

interface g0/1
ip address 10.0.0.1 255.255.255.240
no shutdown
exit

ip route 192.168.1.0 255.255.255.240 192.168.50.1
PC Configuration
PC	IP Address	Subnet Mask	Default Gateway
PC0	192.168.1.10	255.255.255.240	192.168.1.1
PC2	192.168.1.11	255.255.255.240	192.168.1.1
PC1	10.0.0.10	255.255.255.240	10.0.0.1
PC3	10.0.0.11	255.255.255.240	10.0.0.1

Verification Steps
From PC0 or PC2:
bash
Copy
Edit
ping 10.0.0.10
ping 10.0.0.11
From Router0:
bash
Copy
Edit
show ip route
From Switches:
bash
Copy
Edit
show mac address-table
You should see MAC addresses associated with active ports.

