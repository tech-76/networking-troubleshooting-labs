# DNS Troubleshooting

## Overview

DNS stands for Domain Name System. DNS converts human-friendly names, such as websites and server names, into IP addresses that computers use to communicate.

Example:

```text
www.google.com -> 142.250.x.x
fileserver01.company.local -> 192.168.1.20
```

DNS issues can prevent users from accessing websites, internal applications, email, shared drives, VPN resources, and servers by name.

## Purpose

This document explains:

- What DNS does
- Common DNS symptoms
- How to test DNS resolution
- How to flush DNS cache
- How to identify DNS-related issues
- When to escalate DNS problems

## Common Symptoms of DNS Issues

Users may report:

- Websites do not load
- Internal server names do not work
- Shared drive path fails by name
- Email client cannot connect
- VPN connects but internal resources do not resolve
- Browser says DNS address could not be found
- Ping works by IP address but not by name

## DNS Troubleshooting Logic

A simple DNS troubleshooting test:

```text
Can ping 8.8.8.8 but cannot ping google.com?
```

If yes, the device may have network connectivity, but DNS resolution may be failing.

## Step 1: Confirm the Issue

Ask the user:

- What website or server are you trying to reach?
- Are other websites working?
- Are internal resources affected?
- Are you connected to VPN?
- Are other users affected?
- Did the issue start after a network change or password change?

## Step 2: Check IP Configuration

Run:

```cmd
ipconfig /all
```

Look for:

- IPv4 address
- DNS servers
- Default gateway
- DHCP status

Example DNS server entries:

```text
DNS Servers . . . . . . . . . . . : 192.168.1.10
                                    192.168.1.11
```

If DNS servers are missing or incorrect, name resolution may fail.

## Step 3: Test IP Connectivity

Test internet connectivity by IP address:

```cmd
ping 8.8.8.8
```

If this works, the network connection may be working.

Then test name resolution:

```cmd
ping google.com
```

If IP works but name fails, DNS may be the issue.

## Step 4: Use NSLookup

Run:

```cmd
nslookup google.com
```

Example result:

```text
Server:  dns-server.company.local
Address: 192.168.1.10

Non-authoritative answer:
Name: google.com
Address: 142.250.x.x
```

If `nslookup` fails, check:

- DNS server address
- VPN connection
- Local DNS cache
- Network connection
- DNS server availability

## Step 5: Test Internal DNS

For business environments, test internal resources.

Examples:

```cmd
nslookup fileserver01
nslookup fileserver01.company.local
ping fileserver01
```

If public DNS works but internal DNS fails, the issue may involve:

- VPN not connected
- Internal DNS server unreachable
- Wrong DNS suffix
- Split DNS issue
- Domain controller or DNS server issue

## Step 6: Flush DNS Cache

Local DNS cache can store outdated records.

Run:

```cmd
ipconfig /flushdns
```

Then test again:

```cmd
nslookup google.com
ping google.com
```

## Step 7: Renew IP Configuration

If DNS settings come from DHCP, renew the IP lease.

```cmd
ipconfig /release
ipconfig /renew
ipconfig /all
```

Then confirm DNS servers are correct.

## Step 8: Check VPN DNS

Remote users may need VPN to resolve internal systems.

Check:

- VPN is connected
- VPN adapter has correct DNS servers
- Internal resources resolve after connecting
- User is not using a public DNS server only

Common example:

```text
User can access internet but cannot access fileserver01 until VPN is connected.
```

## Step 9: Check Browser vs System DNS

If DNS works in Command Prompt but not in browser:

- Clear browser cache
- Disable browser extensions
- Test another browser
- Check proxy settings
- Check secure DNS browser settings

## Useful Commands

### View network settings

```cmd
ipconfig /all
```

### Flush DNS cache

```cmd
ipconfig /flushdns
```

### Release and renew IP

```cmd
ipconfig /release
ipconfig /renew
```

### Test DNS

```cmd
nslookup google.com
nslookup fileserver01.company.local
```

### Test connection by name

```cmd
ping google.com
ping fileserver01
```

## Common DNS Issues and Fixes

| Issue | Possible Cause | Resolution |
|---|---|---|
| Cannot access websites by name | DNS server issue | Check DNS server settings |
| Can ping IP but not domain name | DNS resolution failure | Flush DNS and check DNS server |
| Internal names fail remotely | VPN not connected | Connect VPN and retest |
| Only one website fails | Website DNS issue or local cache | Flush DNS and test from another device |
| Wrong IP returned | Stale DNS cache or record | Flush cache or escalate |
| DNS servers missing | DHCP issue | Renew IP lease or check DHCP |

## Escalation Criteria

Escalate if:

- Multiple users have DNS issues
- DNS server is unreachable
- Internal domain records are missing
- Domain controller DNS appears down
- Public DNS works but internal DNS fails for many users
- DNS records need to be created, deleted, or changed
- Issue affects production systems

## Example Ticket Note

```text
User reported unable to access internal file server by name.
Confirmed internet access was working.
Ran ipconfig /all and confirmed VPN DNS server was missing.
User reconnected to VPN and received correct DNS settings.
Ran nslookup fileserver01.company.local successfully.
User confirmed access to shared folder restored.
Ticket resolved.
```

## Skills Demonstrated

- DNS troubleshooting
- Name resolution testing
- VPN DNS awareness
- Command-line diagnostics
- Network support documentation
