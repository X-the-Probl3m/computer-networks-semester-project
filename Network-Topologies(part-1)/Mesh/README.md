# Mesh Network Topology
## Overview
In this lab, I demonstrate the implementation of a Mesh Network Topology, connecting four separate LANs using multiple routers.

This setup provides high redundancy and fault tolerance, as every router is connected to every other router. This allows for multiple paths for data transmission; if one link fails, traffic can be rerouted via an alternate path.

 - [Packet File](mesh.pkt)

## Topology

<img width="2001" height="893" alt="image" src="https://github.com/user-attachments/assets/9e2fc95b-9826-4d0b-b4ce-58673e5755f1" />

### Devices used:
- 4 x Routers
- 4 x Switches
- 4 x End devices

## Network Structure
### Router and Interface
| Router | LAN | LAN Interface | To R1 | To R2 | To R3 | To R4 |
|---|---|---|---|---|---|---|
| R1 | 192.168.10.0/24 | 192.168.10.1 | - | 10.0.12.1 (s0/0/0) | 10.0.13.1 (s0/0/1) | 10.0.14.1 (s0/1/0) |
| R2 | 192.168.20.0/24 | 192.168.20.1 | 10.0.12.2 (s0/0/0) | - | 10.0.23.1 (s0/0/1) | 10.0.24.1 (s0/1/0) |
| R3 | 192.168.30.0/24 | 192.168.30.1 | 10.0.13.2 (s0/0/0) | 10.0.23.2 (s0/0/1) | - | 10.0.34.1 (s0/1/0) |
| R4 | 192.168.40.0/24 | 192.168.40.1 | 10.0.14.2 (s0/0/0) | 10.0.24.2 (s0/0/1) | 10.0.34.2 (s0/1/0) | - |

### Subnet Allocation
| Link | Subnet | R1 | R2 | R3 | R4 |
|---|---|---|---|---|---|
| R1-R2 | 10.0.12.0/30 | 10.0.12.1 | 10.0.12.2 | - | - |
| R1-R3 | 10.0.13.0/30 | 10.0.13.1 | - | 10.0.13.2 | - |
| R1-R4 | 10.0.14.0/30 | 10.0.14.1 | - | - | 10.0.14.2 |
| R2-R3 | 10.0.23.0/30 | - | 10.0.23.1 | 10.0.23.2 | - |
| R2-R4 | 10.0.24.0/30 | - | 10.0.24.1 | - | 10.0.24.2 |
| R3-R4 | 10.0.34.0/30 | - | - | 10.0.34.1 | 10.0.34.2 |

### IP Addressing Table
| Device | IP Address | Subnet Mask | Default Gateway | 
|---|---|---|---|
| PC1 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC2 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| PC3 | 192.168.30.10 | 255.255.255.0 | 192.168.30.1 |
| PC4 | 192.168.40.10 | 255.255.255.0 | 192.168.40.1 |

Note: 'R' is for router. e.g R3 stands for Router 3

### Router Configuration (Example for R1)

```
enable
configure terminal
hostname R1

! LAN
interface g0/0
 ip address 192.168.10.1 255.255.255.0
 no shutdown

! To R2
interface s0/0/0
 ip address 10.0.12.1 255.255.255.252
 clock rate 64000
 no shutdown
exit

! To R3
interface s0/0/1
 ip address 10.0.13.1 255.255.255.252
 clock rate 64000
 no shutdown
exit

! To R4
interface s0/1/0
 ip address 10.0.14.1 255.255.255.252
 clock rate 64000
 no shutdown
exit

! OSPF
router ospf 1
 network 192.168.10.0 0.0.0.255 area 0
 network 10.0.12.0 0.0.0.3 area 0
 network 10.0.13.0 0.0.0.3 area 0
 network 10.0.14.0 0.0.0.3 area 0
exit

end
write memory

```
NOTE: All four routers (R1, R2, R3, R4) require similar configuration, but with unique IP addresses for their LAN interfaces. 
OSPF ensures all routers learn each other's networks automatically. It finds the most efficient paths for data to travel.

## Troubleshooting
If devices fail to communicate across different LANs, check the following:
1. Router Interface Status
   - Ensure all physical interfaces on all routers are "up".
2. IP Addressing
   - Double-check all static IP addresses on pc's and router interfaces.




