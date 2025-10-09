# Star Network Topology
## Overview
In this lab, I demonstrate the implementation of a Star Network Topology in Cisco Packet Tracer.
In this setup, five end devices are connected to a central switch.
In a star network, all data passes through the central switch, which then relays it to the intended destination. 

 - [Packet File](Star.pkt)

## Topology

<img width="2001" height="826" alt="image" src="https://github.com/user-attachments/assets/a5737097-e9df-42d7-99be-1a8259bb1df6" />

### Devices used:
- 1 x central switches 
- 5 x end devices 

## IP Addressing Table

| Device | IP Address | Subnet Mask |
|---|---|---|
| PC0 | 192.168.20.1 | 255.255.255.0 |
| PC1 | 192.168.20.2 | 255.255.255.0 |
| PC2 | 192.168.20.3 | 255.255.255.0 |
| PC3 | 192.168.20.4 | 255.255.255.0 |
| PC4 | 192.168.20.5 | 255.255.255.0 |

Each pc is manually assigned an IP address that falls within the 192.168.10.0/24 range.

## Troubleshooting
If pc's fail to communicate, check the following:
 - Ensure all cables are correctly connected (green lights in Packet Tracer).
 - Verify IP addresses and subnet masks are configured correctly.
 - Check for duplicate IP addresses.
 - Make sure the central switch is powered on and functioning.
