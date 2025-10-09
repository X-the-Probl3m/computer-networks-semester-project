# Ring Network Topology
## Overview
In this lab, I demonstrate the implementation of a Ring Network Topology in Cisco Packet Tracer.
In this setup, four switches are connected to one another to form a closed loop (a ring), with each switch connected to a single pc.
In a pure ring topology, data travels in a single direction around the ring. In a switched ring like this, the Spanning Tree Protocol (STP) blocks one link (the orange light) to prevent network loops. This ensures a loop-free logical path while keeping the physical ring intact for redundancy.

 - [Packet File](ring.pkt)

## Topology

<img width="2001" height="830" alt="image" src="https://github.com/user-attachments/assets/5d151623-4d4b-4d76-ac94-dd8ea30b8671" />

### Devices used:
- 4 x switches 
- 4 x end devices 

## IP Addressing Table

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC1 | 192.168.10.1 | 255.255.255.0 | 192.168.20.1 |
| PC2 | 192.168.10.2 | 255.255.255.0 | 192.168.20.1 |
| PC3 | 192.168.10.3 | 255.255.255.0 | 192.168.20.1 |
| PC4 | 192.168.10.4 | 255.255.255.0 | 192.168.20.1 |

Each pc is manually assigned an IP address that falls within the 192.168.10.0/24 range.
The default gateway (192.168.20.1) represents a future connection point to a router or other networks.

## Troubleshooting
If pc's fail to communicate, check the following:
 - Ensure all cables are correctly connected (green lights in Packet Tracer).
 - Verify IP addresses and subnet masks are configured correctly.
 - Check for duplicate IP addresses.
 - Make sure all switches are powered on.

