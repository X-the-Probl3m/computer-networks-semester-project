# Extended Star Network Topology
## Overview
In this lab, I demonstrate the implementation of an Extended Star Network Topology in Cisco Packet Tracer.
In this setup, a central switch connects to multiple secondary switches, each of which connects to several pc's.

 - [Packet File](extended-star.pkt)

## Topology

<img width="2001" height="826" alt="image" src="https://github.com/user-attachments/assets/4395bb34-abe3-47bf-b32c-fc61b1ed0986" />

### Devices used:
- 1 x central switches 
- 5 x secondary switches
- 20 x PCs (4 per secondary switch)

## IP Addressing Table

| Device Range | IP Address | Subnet Mask | Notes |
|---|---|---|---|
| PC0 - PC3 | 192.168.50.10 - 192.168.50.13 | 255.255.255.0 | Connected to Switch1 |
| PC4 - PC7 | 192.168.50.14 - 192.168.50.17 | 255.255.255.0 | Connected to Switch2 |
| PC8 - PC11 | 192.168.50.18 - 192.168.50.21 | 255.255.255.0 | Connected to Switch3 |
| PC12 - PC15 | 192.168.50.22 - 192.168.50.25 | 255.255.255.0 | Connected to Switch4 |
| PC16 - PC19 | 192.168.50.26 - 192.168.50.29 | 255.255.255.0 | Connected to Switch5 |

All devices are sharing the same network (192.168.50.0/24). Each Pc has a unique IP address and subnet mask, manually configured.

## Troubleshooting
If pc's fail to communicate, check the following:
 - Ensure all cables are correctly connected (green lights in Packet Tracer).
 - Verify IP addresses and subnet masks are configured correctly.
 - Check for duplicate IP addresses.
 - Make sure all switches are powered on.
