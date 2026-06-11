# Subnetting Notes

## Overview

Subnetting is the process of dividing a larger network into smaller networks. It helps organize devices, reduce broadcast traffic, improve security, and manage IP address usage.

Subnetting is an important networking skill for help desk, IT support, junior network administrator, and CCNA-level study.

## Purpose

This document explains:

- What subnetting is
- Why subnetting is used
- Common subnet masks
- CIDR notation
- Network and host addresses
- Basic subnetting examples

## Key Terms

| Term | Meaning |
|---|---|
| IP Address | Identifies a device on a network |
| Subnet Mask | Separates network portion and host portion |
| CIDR | Slash notation that shows network bits |
| Network Address | First address in a subnet |
| Broadcast Address | Last address in a subnet |
| Usable Host Range | Addresses assigned to devices |
| Default Gateway | Router address used to leave the subnet |

## Example IP Configuration

```text
IP Address: 192.168.1.25
Subnet Mask: 255.255.255.0
CIDR: /24
Default Gateway: 192.168.1.1
```

This means the device is on the `192.168.1.0/24` network.

## CIDR Notation

CIDR uses a slash to show how many bits are used for the network.

Example:

```text
192.168.1.0/24
```

The `/24` means 24 bits are used for the network portion.

## Common Subnet Masks

| CIDR | Subnet Mask | Total Addresses | Usable Hosts |
|---|---|---:|---:|
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |

Two addresses are usually reserved:

- Network address
- Broadcast address

## Example: /24 Network

Network:

```text
192.168.1.0/24
```

Details:

| Item | Value |
|---|---|
| Network Address | 192.168.1.0 |
| First Usable Host | 192.168.1.1 |
| Last Usable Host | 192.168.1.254 |
| Broadcast Address | 192.168.1.255 |
| Usable Hosts | 254 |

## Example: /25 Network

A `/25` splits a `/24` into two subnets.

Subnet 1:

```text
192.168.1.0/25
```

| Item | Value |
|---|---|
| Network Address | 192.168.1.0 |
| First Usable Host | 192.168.1.1 |
| Last Usable Host | 192.168.1.126 |
| Broadcast Address | 192.168.1.127 |

Subnet 2:

```text
192.168.1.128/25
```

| Item | Value |
|---|---|
| Network Address | 192.168.1.128 |
| First Usable Host | 192.168.1.129 |
| Last Usable Host | 192.168.1.254 |
| Broadcast Address | 192.168.1.255 |

## Example: /26 Network

A `/26` creates blocks of 64 addresses.

Subnets in `192.168.1.0/24`:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

First subnet:

| Item | Value |
|---|---|
| Network Address | 192.168.1.0 |
| First Usable Host | 192.168.1.1 |
| Last Usable Host | 192.168.1.62 |
| Broadcast Address | 192.168.1.63 |
| Usable Hosts | 62 |

## Quick Block Size Method

To find subnet block size:

```text
Block size = 256 - subnet mask value
```

Example:

```text
/26 = 255.255.255.192
256 - 192 = 64
```

So the subnets increase by 64:

```text
0, 64, 128, 192
```

## Why Subnetting Is Used

Subnetting helps with:

- Separating departments
- Improving network organization
- Reducing broadcast traffic
- Supporting VLAN design
- Improving security
- Managing IP address usage
- Supporting routing between networks

Example business layout:

| Department | Subnet |
|---|---|
| HR | 192.168.10.0/24 |
| Sales | 192.168.20.0/24 |
| IT | 192.168.30.0/24 |
| Guest Wi-Fi | 192.168.40.0/24 |

## Troubleshooting With Subnets

If two devices cannot communicate, check:

- Are they in the same subnet?
- Do they have correct subnet masks?
- Do they have the correct default gateway?
- Is routing configured between subnets?
- Is a firewall blocking traffic?
- Are they on the correct VLAN?

Example issue:

```text
Device A: 192.168.1.25 /24
Device B: 192.168.2.25 /24
```

These devices are on different subnets. They need routing through a gateway to communicate.

## Practice Questions

### Question 1

Network:

```text
192.168.5.0/24
```

How many usable hosts?

Answer:

```text
254 usable hosts
```

### Question 2

Network:

```text
192.168.10.0/26
```

What is the block size?

Answer:

```text
256 - 192 = 64
```

### Question 3

Subnets for `192.168.10.0/26`:

Answer:

```text
192.168.10.0
192.168.10.64
192.168.10.128
192.168.10.192
```

## Skills Demonstrated

- Subnet mask understanding
- CIDR notation
- IP address planning
- Network and broadcast address identification
- Host range calculation
- VLAN and routing awareness
- Networking fundamentals
