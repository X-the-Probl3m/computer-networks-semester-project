# Bus Network Topology
## Overview
In this lab, I demonstrate the implementation of a  Bus Network Topology in Cisco Packet Tracer.
In this setup, multiple switches are connected in a linear (bus) arrangement, with each switch connected to a single pc.
In a bus network, all devices are connected to a single shared communication line, allowing data to travel in both directions along the same line. This topology is simple and cost-effective for small networks

 - [Packet File](bus.pkt)

## Topology

<img width="1027" height="342" alt="image" src="https://github.com/user-attachments/assets/2d49d7a3-4362-403e-be76-1bc25fcdd596" />

### Devices used:
- 5 x switches 
- 5 x end devices 

## IP Addressing Table

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC1 | 192.168.10.1 | 255.255.255.0 | 192.168.20.1 |
| PC2 | 192.168.10.2 | 255.255.255.0 | 192.168.20.1 |
| PC3 | 192.168.10.3 | 255.255.255.0 | 192.168.20.1 |
| PC4 | 192.168.10.4 | 255.255.255.0 | 192.168.20.1 |
| PC5 | 192.168.10.5 | 255.255.255.0 | 192.168.20.1 |

Each pc is manually assigned an IP address that falls within the 192.168.10.0/24 range.
The default gateway (192.168.20.1) represents a future connection point to a router or other networks.

## Troubleshooting
If pc's fail to communicate, check the following:
 - Ensure all cables are correctly connected (green lights in Packet Tracer).
 - Verify IP addresses and subnet masks are configured correctly.
 - Check for duplicate IP addresses.
 - Make sure all switches are powered on.
