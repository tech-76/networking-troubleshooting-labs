# DHCP Troubleshooting

## Overview

DHCP stands for Dynamic Host Configuration Protocol. DHCP automatically assigns IP addresses and network settings to devices.

Without DHCP, users may need manual IP settings. In most business networks, DHCP provides IP addresses, subnet masks, default gateways, and DNS server addresses.

## Purpose

This document explains:

- What DHCP does
- How the DHCP process works
- Common DHCP problems
- Troubleshooting steps
- Useful commands
- Escalation criteria

## What DHCP Provides

DHCP can provide:

| Setting | Example | Purpose |
|---|---|---|
| IP Address | 192.168.1.25 | Identifies the device |
| Subnet Mask | 255.255.255.0 | Identifies local network size |
| Default Gateway | 192.168.1.1 | Allows access outside local network |
| DNS Server | 192.168.1.10 | Resolves names to IP addresses |
| Lease Time | 8 hours | How long the address is assigned |

## DHCP Process

The basic DHCP process is often called DORA.

| Step | Meaning | Description |
|---|---|---|
| Discover | Client searches | Device looks for a DHCP server |
| Offer | Server responds | DHCP server offers an IP address |
| Request | Client accepts | Device requests the offered IP |
| Acknowledge | Server confirms | DHCP server confirms the lease |

## Common DHCP Symptoms

Users may report:

- No internet access
- Cannot connect to network
- Wi-Fi connected but no internet
- Device has 169.254.x.x IP address
- Cannot access shared drives
- Cannot reach default gateway
- Network works for some users but not others

## What Is a 169.254.x.x Address?

A `169.254.x.x` address is an Automatic Private IP Addressing address, also called APIPA.

Example:

```text
169.254.10.25
```

This usually means the computer could not get an IP address from DHCP.

## Step 1: Check IP Configuration

Run:

```cmd
ipconfig /all
```

Look for:

- IPv4 address
- DHCP enabled
- DHCP server
- Default gateway
- DNS servers

Example healthy configuration:

```text
IPv4 Address: 192.168.1.25
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.1.1
DHCP Server: 192.168.1.5
DNS Servers: 192.168.1.10
```

Example DHCP issue:

```text
IPv4 Address: 169.254.20.18
Default Gateway: blank
DHCP Server: blank
```

## Step 2: Confirm Network Connection

For wired devices:

- Check Ethernet cable
- Check docking station
- Check switch port lights
- Try another cable
- Try another network port

For Wi-Fi:

- Confirm correct Wi-Fi network
- Turn Wi-Fi off and on
- Forget and reconnect to Wi-Fi
- Move closer to access point
- Restart device

## Step 3: Release and Renew IP Address

Run Command Prompt as user or administrator:

```cmd
ipconfig /release
ipconfig /renew
```

Then check:

```cmd
ipconfig /all
```

If the device receives a valid IP address, test network access.

## Step 4: Disable and Re-Enable Network Adapter

Open Network Connections:

```cmd
ncpa.cpl
```

Then:

1. Right-click the network adapter.
2. Select **Disable**.
3. Wait a few seconds.
4. Right-click again.
5. Select **Enable**.

Then run:

```cmd
ipconfig /renew
```

## Step 5: Restart the Computer

A restart can clear temporary network issues.

After restart:

1. Connect to network.
2. Run `ipconfig /all`.
3. Confirm valid IP settings.
4. Test internet and internal resources.

## Step 6: Check DHCP Scope or Server

If multiple users are affected, the issue may be on the DHCP server side.

Possible causes:

- DHCP server offline
- DHCP scope full
- DHCP service stopped
- VLAN DHCP relay issue
- Network switch issue
- Incorrect DHCP options
- IP conflict

Help desk technicians may need to escalate this to a network or systems administrator.

## Step 7: Check for Static IP Settings

A device may have incorrect manual IP settings.

1. Open Network Connections with:

```cmd
ncpa.cpl
```

2. Open adapter properties.
3. Select **Internet Protocol Version 4 (TCP/IPv4)**.
4. Confirm whether the device uses:
   - Obtain an IP address automatically
   - Obtain DNS server address automatically

If company policy requires DHCP, set to automatic only with approval.

## Useful Commands

### View IP configuration

```cmd
ipconfig /all
```

### Release IP address

```cmd
ipconfig /release
```

### Renew IP address

```cmd
ipconfig /renew
```

### Flush DNS

```cmd
ipconfig /flushdns
```

### Open network adapters

```cmd
ncpa.cpl
```

### Test gateway

```cmd
ping 192.168.1.1
```

## Common DHCP Issues and Fixes

| Issue | Possible Cause | Resolution |
|---|---|---|
| 169.254.x.x address | DHCP not reached | Check connection and renew IP |
| No default gateway | DHCP option missing | Renew IP or escalate |
| Wrong IP range | Connected to wrong network | Reconnect to correct Wi-Fi/VLAN |
| IP conflict | Duplicate IP address | Release/renew IP and escalate |
| Multiple users affected | DHCP server or scope issue | Escalate to network/admin team |
| Static IP set incorrectly | Manual configuration error | Change to DHCP if approved |

## Escalation Criteria

Escalate if:

- Multiple users receive 169.254.x.x addresses
- DHCP scope may be full
- DHCP server is unreachable
- VLAN or switch configuration may be involved
- IP conflicts continue
- DHCP options are incorrect
- Business-critical devices cannot obtain IP addresses

## Example Ticket Note

```text
User reported no internet connection.
Ran ipconfig /all and found 169.254.x.x APIPA address.
Confirmed Wi-Fi was connected but device did not receive DHCP lease.
Forgot and reconnected to approved Wi-Fi network.
Ran ipconfig /renew and confirmed valid IP address, gateway, and DNS.
User confirmed internet and email access restored.
Ticket resolved.
```

## Skills Demonstrated

- DHCP troubleshooting
- IP address diagnostics
- Network adapter support
- APIPA identification
- Command-line troubleshooting
- Escalation awareness
- Support documentation
