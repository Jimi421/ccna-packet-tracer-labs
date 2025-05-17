🌐 OSPF Area 1 Routing Lab (Full Mesh, 3 Routers)

Scenario

You are tasked with configuring dynamic routing between three branch networks using OSPF Area 1. Each site contains PCs, servers, or printers on its local LAN. The routers form a full mesh topology, providing path redundancy and demonstrating OSPF convergence and route learning.

Topology Summary

Routers: R1, R2, R3 (Cisco 2911)

Switches: SW1, SW2, SW3 (2960)

Devices: PCs, Printer, File Server, Laptop

🌐 OSPF Point-to-Point Links

Link

Interfaces

Subnet

R1 ↔ R2

R1 G0/0 ↔ R2 G0/0

192.168.10.0/30

R2 ↔ R3

R2 G0/2 ↔ R3 G0/0

192.168.20.0/30

R1 ↔ R3

R1 G0/2 ↔ R3 G0/2

192.168.30.0/30

🚀 LAN Networks

Site

Router Interface

Subnet

Devices

Site A

R1 G0/1

10.1.1.0/28

PC1, PC2

Site B

R2 G0/1

10.2.2.0/28

Laptop1, File Server

Site C

R3 G0/1

10.3.3.0/28

Office PC, Laser Printer

💡 Router Configurations

R1

interface g0/0
 ip address 192.168.10.1 255.255.255.252
 no shutdown
interface g0/1
 ip address 10.1.1.1 255.255.255.240
 no shutdown
interface g0/2
 ip address 192.168.30.1 255.255.255.252
 no shutdown

router ospf 1
 network 192.168.10.0 0.0.0.3 area 1
 network 192.168.30.0 0.0.0.3 area 1
 network 10.1.1.0 0.0.0.15 area 1

R2

interface g0/0
 ip address 192.168.10.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 10.2.2.1 255.255.255.240
 no shutdown
interface g0/2
 ip address 192.168.20.1 255.255.255.252
 no shutdown

router ospf 1
 network 192.168.10.0 0.0.0.3 area 1
 network 192.168.20.0 0.0.0.3 area 1
 network 10.2.2.0 0.0.0.15 area 1

R3

interface g0/0
 ip address 192.168.20.2 255.255.255.252
 no shutdown
interface g0/1
 ip address 10.3.3.1 255.255.255.240
 no shutdown
interface g0/2
 ip address 192.168.30.2 255.255.255.252
 no shutdown

router ospf 1
 network 192.168.20.0 0.0.0.3 area 1
 network 192.168.30.0 0.0.0.3 area 1
 network 10.3.3.0 0.0.0.15 area 1

💻 End Device IP Settings

Device

IP Address

Default Gateway

PC1

10.1.1.10

10.1.1.1

PC2

10.1.1.11

10.1.1.1

Laptop1

10.2.2.10

10.2.2.1

File Server

10.2.2.11

10.2.2.1

Office PC

10.3.3.10

10.3.3.1

Laser Printer

10.3.3.11

10.3.3.1

🔍 Verification

On Routers:

show ip ospf neighbor
show ip route ospf

2 OSPF neighbors per router

Full dynamic route visibility

On PCs:

ping 10.2.2.10
ping 10.3.3.10
ping 10.1.1.10

End-to-end connectivity between all networks