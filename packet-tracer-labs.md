# Cisco Packet Tracer Labs

## Overview

Cisco Packet Tracer is a network simulation tool used to practice networking concepts such as routing, switching, IP addressing, VLANs, DHCP, DNS, wireless networks, and basic network troubleshooting.

This document lists practical Packet Tracer lab ideas that can be used to build hands-on networking skills for IT support, help desk, junior network administrator, and CCNA-level learning.

## Purpose

This document demonstrates:

- Hands-on networking practice
- IP addressing skills
- Router and switch configuration awareness
- VLAN and DHCP concepts
- Troubleshooting practice
- Lab documentation ability

## Recommended Lab Format

Each lab should include:

- Lab name
- Objective
- Network topology
- IP addressing table
- Configuration steps
- Testing steps
- Troubleshooting notes
- Screenshots, if available
- Final result

## Lab 1: Basic LAN Connectivity

### Objective

Create a basic local area network with two PCs connected to a switch.

### Devices

- 2 PCs
- 1 switch
- Copper straight-through cables

### IP Addressing

| Device | IP Address | Subnet Mask |
|---|---|---|
| PC1 | 192.168.1.10 | 255.255.255.0 |
| PC2 | 192.168.1.11 | 255.255.255.0 |

### Testing

From PC1:

```text
ping 192.168.1.11
```

Expected result:

```text
Successful replies from PC2
```

### Skills Practiced

- Basic LAN setup
- IP addressing
- Switch connectivity
- Ping testing

## Lab 2: Router Between Two Networks

### Objective

Connect two different networks using a router.

### Devices

- 2 PCs
- 1 router
- 2 switches

### IP Addressing

| Device | Interface | IP Address | Subnet Mask | Gateway |
|---|---|---|---|---|
| PC1 | NIC | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC2 | NIC | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| Router | G0/0 | 192.168.10.1 | 255.255.255.0 | N/A |
| Router | G0/1 | 192.168.20.1 | 255.255.255.0 | N/A |

### Testing

From PC1:

```text
ping 192.168.20.10
```

Expected result:

```text
PC1 can reach PC2 through the router
```

### Skills Practiced

- Routing between networks
- Default gateway configuration
- Interface IP addressing
- Ping testing

## Lab 3: DHCP Server on Router

### Objective

Configure a router to assign IP addresses automatically using DHCP.

### Example DHCP Scope

```text
Network: 192.168.30.0/24
Default Gateway: 192.168.30.1
DNS Server: 8.8.8.8
Excluded Addresses: 192.168.30.1 - 192.168.30.10
```

### Example Router Commands

```text
ip dhcp excluded-address 192.168.30.1 192.168.30.10
ip dhcp pool LAN30
 network 192.168.30.0 255.255.255.0
 default-router 192.168.30.1
 dns-server 8.8.8.8
```

### Testing

On PC:

```text
Set IP configuration to DHCP
Confirm device receives IP address
Ping default gateway
```

### Skills Practiced

- DHCP configuration
- IP lease testing
- Default gateway setup
- DNS option awareness

## Lab 4: VLAN Basics

### Objective

Create two VLANs and assign switch ports to each VLAN.

### VLAN Plan

| VLAN | Name | Network |
|---|---|---|
| 10 | Sales | 192.168.10.0/24 |
| 20 | IT | 192.168.20.0/24 |

### Example Switch Commands

```text
vlan 10
 name Sales
vlan 20
 name IT

interface fa0/1
 switchport mode access
 switchport access vlan 10

interface fa0/2
 switchport mode access
 switchport access vlan 20
```

### Testing

- Devices in same VLAN should communicate.
- Devices in different VLANs need routing to communicate.

### Skills Practiced

- VLAN creation
- Access port assignment
- Network segmentation
- Basic switching

## Lab 5: Inter-VLAN Routing

### Objective

Allow devices in different VLANs to communicate using router-on-a-stick.

### Example Subinterfaces

```text
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0

interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
```

### Testing

From Sales PC:

```text
ping 192.168.20.10
```

Expected result:

```text
Sales VLAN can communicate with IT VLAN through router
```

### Skills Practiced

- Trunking concept
- Router-on-a-stick
- VLAN gateway configuration
- Inter-VLAN routing

## Lab 6: DNS Server Practice

### Objective

Configure a DNS server in Packet Tracer and test name resolution.

### Example DNS Record

```text
Name: www.company.local
Address: 192.168.50.10
```

### Testing

From PC:

```text
ping www.company.local
```

Expected result:

```text
Name resolves to IP address and ping succeeds
```

### Skills Practiced

- DNS record setup
- Name resolution
- Client DNS settings
- Troubleshooting DNS

## Lab 7: Wireless Network Setup

### Objective

Create a basic wireless network with a wireless router and laptop clients.

### Configuration

- SSID: Company-WiFi
- Security: WPA2
- DHCP: Enabled
- Network: 192.168.100.0/24

### Testing

- Connect laptop to SSID
- Confirm DHCP address
- Ping default gateway
- Ping another wireless client

### Skills Practiced

- Wireless configuration
- SSID setup
- WPA2 security
- DHCP testing

## Lab 8: Network Troubleshooting Challenge

### Objective

Fix a broken network where users cannot communicate.

### Possible Issues to Build Into the Lab

- Wrong IP address
- Wrong subnet mask
- Missing default gateway
- Incorrect VLAN assignment
- Shutdown router interface
- Wrong cable type
- Missing DHCP configuration
- Wrong DNS server

### Troubleshooting Commands

```text
ping
show ip interface brief
show vlan brief
show running-config
show ip route
```

### Skills Practiced

- Troubleshooting process
- Router and switch verification
- IP addressing review
- VLAN review
- Documentation

## Example Lab Documentation Template

```text
Lab Name:
Objective:
Devices Used:
IP Addressing Table:
Configuration Steps:
Testing Steps:
Issue Found:
Resolution:
Final Result:
Skills Practiced:
```

## Example GitHub Lab Summary

```text
Built a Packet Tracer lab with two VLANs, router-on-a-stick inter-VLAN routing, and DHCP addressing.
Configured VLAN 10 for Sales and VLAN 20 for IT.
Verified connectivity using ping and show commands.
Troubleshot incorrect gateway configuration and confirmed successful communication between VLANs.
```

## Skills Demonstrated

- Cisco Packet Tracer practice
- Router and switch basics
- IP addressing
- DHCP configuration
- DNS practice
- VLAN concepts
- Inter-VLAN routing
- Troubleshooting and documentation
