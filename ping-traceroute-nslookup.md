# Ping, Traceroute, and NSLookup

## Overview

`ping`, `tracert`, and `nslookup` are common command-line tools used to troubleshoot network connectivity and DNS issues.

These tools are useful for help desk technicians, desktop support technicians, network administrators, and systems administrators.

## Purpose

This document explains:

- What each command does
- When to use each command
- How to read basic results
- Common troubleshooting examples
- Ticket documentation examples

## Tool Summary

| Tool | Windows Command | Purpose |
|---|---|---|
| Ping | `ping` | Tests basic connectivity |
| Traceroute | `tracert` | Shows network path to destination |
| NSLookup | `nslookup` | Tests DNS name resolution |
| IPConfig | `ipconfig` | Shows local IP settings |

## Ping

`ping` tests whether a device can reach another device over the network.

Example:

```cmd
ping google.com
```

Example by IP address:

```cmd
ping 8.8.8.8
```

## When to Use Ping

Use ping to check:

- Internet connectivity
- Local gateway connectivity
- Server reachability
- Printer reachability
- DNS vs IP connectivity
- Packet loss or latency

## Ping Example Results

Successful ping:

```text
Reply from 8.8.8.8: bytes=32 time=15ms TTL=117
```

Failed ping:

```text
Request timed out.
```

Unknown host:

```text
Ping request could not find host google.com.
```

## Ping Troubleshooting Logic

Test in this order:

### 1. Ping loopback address

```cmd
ping 127.0.0.1
```

This tests the local TCP/IP stack.

### 2. Ping own IP address

```cmd
ping 192.168.1.25
```

This tests the local network adapter.

### 3. Ping default gateway

```cmd
ping 192.168.1.1
```

This tests local network connectivity.

### 4. Ping public IP

```cmd
ping 8.8.8.8
```

This tests internet connectivity by IP.

### 5. Ping domain name

```cmd
ping google.com
```

This tests DNS and connectivity.

## Tracert

`tracert` shows the path traffic takes to a destination.

Windows command:

```cmd
tracert google.com
```

The result shows each network hop between the computer and destination.

## When to Use Tracert

Use `tracert` when:

- A website is slow or unreachable
- You want to see where traffic stops
- VPN traffic may be taking the wrong route
- Internal resources are unreachable
- You need to identify routing path issues

## Tracert Example

```text
1    2 ms    1 ms    1 ms  192.168.1.1
2   10 ms   11 ms   10 ms  isp-gateway
3   15 ms   14 ms   15 ms  destination-network
```

If the trace stops at the first hop, the issue may be local network or gateway related.

If the trace reaches several hops and then fails, the issue may be further upstream.

## NSLookup

`nslookup` tests DNS resolution.

Example:

```cmd
nslookup google.com
```

Example internal lookup:

```cmd
nslookup fileserver01.company.local
```

## When to Use NSLookup

Use `nslookup` when:

- Website names do not resolve
- Internal server names fail
- DNS server may be wrong
- VPN connects but internal names fail
- A user can ping IP addresses but not names

## NSLookup Example

```text
Server:  dns.company.local
Address: 192.168.1.10

Name: google.com
Address: 142.250.x.x
```

If DNS fails, possible causes include:

- Incorrect DNS server
- VPN not connected
- DNS server unavailable
- Stale DNS cache
- Missing DNS record

## IPConfig

`ipconfig` shows local network configuration.

```cmd
ipconfig /all
```

Important fields:

- IPv4 address
- Subnet mask
- Default gateway
- DNS servers
- DHCP enabled
- DHCP server

## Useful Command List

### Ping gateway

```cmd
ping 192.168.1.1
```

### Ping public IP

```cmd
ping 8.8.8.8
```

### Ping website

```cmd
ping google.com
```

### Trace route

```cmd
tracert google.com
```

### DNS lookup

```cmd
nslookup google.com
```

### View IP configuration

```cmd
ipconfig /all
```

### Flush DNS

```cmd
ipconfig /flushdns
```

### Renew IP address

```cmd
ipconfig /release
ipconfig /renew
```

## Common Scenarios

### Scenario 1: Internet Not Working

Steps:

```cmd
ipconfig /all
ping 192.168.1.1
ping 8.8.8.8
ping google.com
```

Possible finding:

```text
Can ping gateway but cannot ping 8.8.8.8.
```

Possible cause:

```text
Internet or upstream network issue.
```

### Scenario 2: DNS Issue

Steps:

```cmd
ping 8.8.8.8
ping google.com
nslookup google.com
```

Possible finding:

```text
Can ping 8.8.8.8 but cannot resolve google.com.
```

Possible cause:

```text
DNS issue.
```

### Scenario 3: Internal Server Not Available

Steps:

```cmd
ping fileserver01
nslookup fileserver01
tracert fileserver01
```

Possible finding:

```text
Internal name does not resolve while remote.
```

Possible cause:

```text
VPN not connected or VPN DNS issue.
```

## Common Results and Meaning

| Result | Meaning |
|---|---|
| Reply from address | Destination responded |
| Request timed out | No response received |
| Destination host unreachable | Route or gateway issue |
| Could not find host | DNS name resolution failed |
| High latency | Slow response or network congestion |
| Packet loss | Network instability |
| Trace stops early | Routing or firewall issue |

## Example Ticket Note

```text
User reported unable to access internal file server.
Ran ipconfig /all and confirmed valid IP address.
Ping to gateway was successful.
Ping to public IP was successful.
Nslookup for fileserver01 failed while user was disconnected from VPN.
User connected VPN and internal DNS lookup succeeded.
User confirmed file server access restored.
Ticket resolved.
```

## Skills Demonstrated

- Network command-line troubleshooting
- DNS testing
- Connectivity testing
- Routing path review
- Help desk diagnostics
- Technical documentation
