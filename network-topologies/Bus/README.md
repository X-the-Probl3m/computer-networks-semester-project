# Bus Topology

## Overview
This project demonstrates a Bus Topology implemented in Cisco Packet Tracer.
In a bus network, all devices are connected to a single shared communication line, allowing data to travel in both directions along the same backbone.
This setup uses switches connected in a straight line to simulate the shared medium instead of a single coaxial cable as in traditional bus networks.

<img width="1027" height="342" alt="image" src="https://github.com/user-attachments/assets/2d49d7a3-4362-403e-be76-1bc25fcdd596" />

## Topology Description
- 5 switches connected in a single straight line
- Each pc connects to its respective switch
- All devices share the same IP network (192.168.10.0/24) 

## Network Configuration

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC1 | 192.168.10.1 | 255.255.255.0 | 192.168.20.1 |
| PC2 | 192.168.10.2 | 255.255.255.0 | 192.168.20.1 |
| PC3 | 192.168.10.3 | 255.255.255.0 | 192.168.20.1 |
| PC4 | 192.168.10.4 | 255.255.255.0 | 192.168.20.1 |
| PC5 | 192.168.10.5 | 255.255.255.0 | 192.168.20.1 |
