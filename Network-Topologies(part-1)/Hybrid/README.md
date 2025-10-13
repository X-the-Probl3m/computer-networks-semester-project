# Hybrid Network
## Overview
In this lab, I design and implement a hybrid network that integrates the five previously studied topologies — bus, star, ring, extended star, and mesh — into one cohesive network.
The objective was to configure IPv4 and IPv6 addressing, implement VLAN segmentation, and set up multiple network services to ensure dynamic and efficient host configuration.

The network includes four servers providing core services:
- DHCPv4 Server
- DHCPv6 Server
- DNS Server
- HTTP Server

This setup demonstrates how enterprise networks can integrate dual-stack (IPv4/IPv6) communication with automated address assignment and VLAN-based segmentation for scalability and security.

- [Packet File](hybrid.pkt)

## Topology

<img width="1447" height="718" alt="hybrid_topology" src="https://github.com/user-attachments/assets/f36dd584-6491-44cc-acab-9b805bddcafc" />

### Devices used:
- 1 x Multilayer Switch (core)
- 14 x 2960 Switches (Access distribution)
- 4 x Servers (DHCPv4. DHCPv6, DNS, HTTP)
- 10 x PCs (End devices)

## VLAN and IP Addressing Structure
| VLAN | Purpose | SVI (IPv4) | SVI (IPv6) | DHCPv4 Pool | IPv6 Prefix | Start IP | Max Number of Users |
|---|---|---|---|---|---|---|---|
| VLAN 1 | Server network (ring) | 192.168.1.1 | 2001:db8:acad:1::/64 | serverPOOL | 2001:db8:acad:1::/64 | 192.168.1.10 | 20 |
| VLAN 10 | Admin (star) | 192.168.10.1 | 2001:db8:acad:10::/64 | VLAN10 | 2001:db8:acad:10::/64 | 192.168.10.10 | 20 |
| VLAN 20 | Sales (mesh) | 192.168.20.1 | 2001:db8:acad:20::/64 | VLAN20 | 2001:db8:acad:20::/64 | 192.168.20.10 | 20|
| VLAN 30 | Trading floor (bus) | 192.168.30.1 | 2001:db8:acad:30::/64 | VLAN30 | 2001:db8:acad:30::/64 | 192.168.30.10 | 20 |

### Static IP Addresses
| Device | IPv4 | IPv6 |
|---|---|---|
| DHCPv4 Server | 192.168.1.2 | 2001:db8:acad:1::2 |
| DHCPv6 Server | 192.168.1.5 | 2001:db8:acad:1::5 |
| DNS Server | 192.168.1.3 | 2001:db8:acad:1::3 |
| HTTP Server | 192.168.1.4 | 2001:db8:acad:1::4 |

## Multilayer Switch Configuration

```
enable
conf t
ipv6 unicast-routing

! VLAN 1
int vlan 1
 ip address 192.168.1.1 255.255.255.0
 ipv6 address 2001:db8:acad:1::1/64
 no shutdown

! VLAN 10
int vlan 10
 ip address 192.168.10.1 255.255.255.0
 ipv6 address 2001:db8:acad:10::1/64
 no shutdown

! VLAN 20
int vlan 20
 ip address 192.168.20.1 255.255.255.0
 ipv6 address 2001:db8:acad:20::1/64
 no shutdown

! VLAN 30
int vlan 30
 ip address 192.168.30.1 255.255.255.0
 ipv6 address 2001:db8:acad:30::1/64
 no shutdown

! DHCP relay configuration
int vlan 10
 ip helper-address 192.168.1.2
int vlan 20
 ip helper-address 192.168.1.2
int vlan 30
 ip helper-address 192.168.1.2

end
write memory
```

##Testing and Verification 
| Device | VLAN | Expected IPv4 | Expected IPv6 | Default Gateway | Verification |
|---|---|---|---|---|---|
| PC in VLAN 1 | 1 | 192.168.1.x | 2001:db8:acad:1::x | 192.168.1.1 | ipconfig + ping 192.168.1.1 | 
| PCs in VLAN 10 | 10 | 192.168.10.x | 2001:db8:acad:10::x | 192.168.10.1 | ipconfig + ping 192.168.10.1 | 
| PCs in VLAN 20 | 20 | 192.168.20.x | 2001:db8:acad:20::x | 192.168.20.1 | ipconfig + ping 192.168.20.1 |
| PCs in VLAN 30 | 30 | 192.168.30.x | 2001:db8:acad:30::x | 192.168.30.1 | ipconfig + ping 192.168.30.1 | 

'x' represents a valid host number within the subnets IP address range. 
If all devices receive IP addresses dynamically (both IPv4 & IPv6) and can reach the default gateway, DNS, and HTTP server, then the configuration is successful.

## Troubleshooting
If hosts fail to obtain IP addresses or cannot reach servers check the following:
1. DHCP Configuration
   - Ensure DHCP services are active on the servers.
   - Verify each pool matches its correct VLAN gateway and DNS address
2. VLAN Assignment
   - run `show vlan brief` on the switch to confirm PCs are in the correct VLAN.
   - Ensure trunks between switches and the multilayer switch allow all VLANs.
3. Relay Configuration
   - Check that `ip helper-address` is configured under the correct VLAN interface.
4. IPv6 Settings
   - Confirm each interface has the proper IPv6 prefix and that RA (Router Advertisement) is enabled.
5. End Device Settings
   - Ensure PCs are set to obtain IP addresses automatically for both IPv4 and IPv6.




