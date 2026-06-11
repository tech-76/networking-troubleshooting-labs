# TCP/IP Basics

## Overview

TCP/IP stands for Transmission Control Protocol / Internet Protocol. It is the main set of networking protocols used to allow computers, servers, printers, routers, and other devices to communicate across networks.

TCP/IP is used in local area networks, wide area networks, the internet, VPN connections, cloud services, email, websites, file sharing, and most modern business systems.

## Purpose

This document explains:

- What TCP/IP is
- Why IP addresses are used
- Difference between TCP and UDP
- Common ports and protocols
- Basic troubleshooting steps
- Useful Windows commands

## What Is TCP/IP?

TCP/IP is a protocol suite. A protocol is a set of rules that devices follow to communicate.

TCP/IP allows devices to:

- Send and receive data
- Identify each other using IP addresses
- Route traffic between networks
- Use ports to connect to services
- Break data into packets and reassemble it

## IP Address Basics

An IP address identifies a device on a network.

Example IPv4 address:

```text
192.168.1.25
```

An IPv4 address usually works with:

| Item | Example | Purpose |
|---|---|---|
| IP Address | 192.168.1.25 | Identifies the device |
| Subnet Mask | 255.255.255.0 | Identifies the local network size |
| Default Gateway | 192.168.1.1 | Sends traffic outside the local network |
| DNS Server | 192.168.1.10 | Resolves names to IP addresses |

## Private IP Address Ranges

Private IP addresses are commonly used inside homes and businesses.

| Range | Example |
|---|---|
| 10.0.0.0 - 10.255.255.255 | 10.0.0.25 |
| 172.16.0.0 - 172.31.255.255 | 172.16.5.20 |
| 192.168.0.0 - 192.168.255.255 | 192.168.1.25 |

Private IP addresses are not directly routed on the public internet. They usually use NAT through a router or firewall.

## TCP vs UDP

### TCP

TCP is connection-oriented. It confirms that data is delivered correctly.

Common uses:

- Web browsing using HTTPS
- Email
- File transfers
- Remote desktop
- Database connections

TCP is reliable because it checks delivery and retransmits missing data.

### UDP

UDP is connectionless. It sends data quickly but does not guarantee delivery.

Common uses:

- Voice calls
- Video streaming
- DNS lookups
- Online gaming
- Some VPN traffic

UDP is faster but less reliable than TCP.

## Common Ports and Protocols

| Port | Protocol | Service |
|---|---|---|
| 20/21 | TCP | FTP |
| 22 | TCP | SSH |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 67/68 | UDP | DHCP |
| 80 | TCP | HTTP |
| 123 | UDP | NTP |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |
| 445 | TCP | SMB file sharing |
| 3389 | TCP | Remote Desktop Protocol |

## How Devices Communicate

Example: A user opens a website.

1. User enters a website name.
2. DNS resolves the name to an IP address.
3. The computer sends traffic to the destination IP.
4. If the destination is outside the local network, traffic goes to the default gateway.
5. The router forwards the traffic.
6. The website responds.
7. The browser displays the page.

## Basic TCP/IP Troubleshooting Process

When a user reports a network issue, check:

1. Physical connection or Wi-Fi
2. IP address
3. Default gateway
4. DNS server
5. Local network connectivity
6. Internet connectivity
7. DNS resolution
8. Firewall or VPN status

## Useful Commands

### View IP Configuration

```cmd
ipconfig /all
```

Check:

- IPv4 address
- Subnet mask
- Default gateway
- DNS servers
- DHCP enabled status

### Test Local Network

```cmd
ping 192.168.1.1
```

This tests connectivity to the default gateway.

### Test Internet by IP Address

```cmd
ping 8.8.8.8
```

If this works, the device likely has network connectivity.

### Test DNS Resolution

```cmd
ping google.com
```

If `ping 8.8.8.8` works but `ping google.com` fails, DNS may be the issue.

### Trace Network Path

```cmd
tracert google.com
```

This shows the path traffic takes to reach a destination.

### DNS Lookup

```cmd
nslookup google.com
```

This checks DNS name resolution.

## Common TCP/IP Issues

| Issue | Possible Cause | Fix |
|---|---|---|
| 169.254.x.x address | DHCP failed | Release/renew IP or check DHCP server |
| No default gateway | Bad network configuration | Check DHCP or manual IP settings |
| Can ping IP but not name | DNS issue | Flush DNS or check DNS server |
| Cannot reach gateway | Local network issue | Check Wi-Fi, Ethernet, or adapter |
| Slow connection | Network congestion or weak Wi-Fi | Test wired connection or check signal |
| Internal resources unavailable | VPN disconnected | Connect VPN and retest |

## Ticket Documentation Example

```text
User reported no internet connection.
Checked IP configuration using ipconfig /all.
Device had valid IP address but DNS lookup failed.
Flushed DNS cache and confirmed DNS server settings.
User was able to access websites after reconnecting to network.
Ticket resolved.
```

## Skills Demonstrated

- TCP/IP fundamentals
- IP addressing basics
- Port and protocol awareness
- Network troubleshooting
- Command-line diagnostics
- Help desk documentation
