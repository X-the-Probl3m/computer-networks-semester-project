# DHCPv4 Server Configuration
## Overview
In this lab, I configure a DHCPv4 server to automatically assign IPv4 addresses to clients on multiple LANs. 

## Topology


### Devices used:
- 1 x DHCP Server
- 1 x Router
- 2 x Switches
- 6 x End Devices

### Network Structure: 
- LAN 1: Connected to GigabitEthernet0/0
- LAN 2: Conected to GigabitEthernet0/1
- DHCP Server: Connected to the switch on LAN 1

## IP Addressing Table
| Network | Router Interface | Default Gateway | IP Range | 
|---|---|---|---|
| LAN 1 | G0/0 | 192.168.20.1 | 192.168.20.3 - 192.168.20.22 |
| LAN 2 | G0/1 | 192.168.30.1 | 192.168.30.2 - 192.168.30.21 |

## Router Configuration

```
enable
conf t

! LAN 1 Configuration
int g0/0
ip address 192.168.20.1 255.255.255.0
ip helper-address 192.168.20.2
no shutdown
do write memory
exit

! LAN 2 Configuration
int g0/1
ip address 192.168.30.1 255.255.255.0
ip helper-address 192.168.20.2
no shutdown
do write memory
exit

exit
write memory
```

The `ip helper-address` command forwards DHCP broadcast requests to the DHCP server

## DHCPv4 Server Configuration
### Pool 1 -LAN 1
| Setting | Value |
|---|---|
| Pool name | LAN 1 |
| Default Gateway | 192.168.20.1 |
| Start IP | 192.168.20.3 |
| Subnet Mask | 255.255.255.0 |
| Max Users | 20 |

### Pool 2 -LAN 2
| Setting | Value |
|---|---|
| Pool name | LAN 2 |
| Default Gateway | 192.168.30.1 |
| Start IP | 192.168.30.2 |
| Subnet Mask | 255.255.255.0 |
| Max Users | 20 |

## Testing and Verification
| Device | Expected IP | Gateway | Verification |
|---|---|---|---|
| PC0 - PC2 | 192.168.20.x | 192.168.20.1 | `ipconfig` then `ping` 192.168.20.1 |
| Laptop0 - Laptop2 | 192.168.30.x | 192.168.30.1 | `ipconfig` then `ping` 192.168.30.1 |


'x' represents a  valid host address within the assigned ip address range 
If all devices receive IP addresses dynamically and can communicate with the router and each other, DHCPv4 is  functioning correctly.




