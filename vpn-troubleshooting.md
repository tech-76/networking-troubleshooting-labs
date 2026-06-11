# VPN Troubleshooting

## Overview

A VPN, or Virtual Private Network, allows users to securely connect to company resources from outside the office. VPN connections are commonly used by remote and hybrid workers to access internal applications, shared drives, intranet websites, and administrative systems.

VPN issues are common help desk and desktop support requests.

## Purpose

This document explains:

- Common VPN symptoms
- Basic VPN troubleshooting steps
- Account and password checks
- Network and DNS testing
- MFA-related checks
- Escalation criteria
- Example ticket notes

## Common VPN Symptoms

Users may report:

- VPN will not connect
- VPN disconnects often
- VPN connects but shared drives do not work
- VPN connects but internal websites do not load
- VPN authentication fails
- MFA prompt does not appear
- VPN is slow
- User can access internet but not company resources

## Step 1: Gather Information

Ask the user:

- Are you working remotely or in the office?
- What VPN client are you using?
- What error message do you see?
- Did your password recently change?
- Does your internet work without VPN?
- Are you receiving MFA prompts?
- Can you access some resources or none?
- When did the issue start?

## Step 2: Confirm Internet Access

VPN requires a working internet connection.

Test:

```cmd
ping 8.8.8.8
ping google.com
```

If internet does not work, fix the local network issue first.

## Step 3: Confirm VPN Client Status

Check:

- VPN app opens correctly
- Correct VPN profile is selected
- Username is correct
- Password is correct
- MFA is completed
- VPN does not show expired certificate or policy errors
- VPN client is updated, if required by company policy

## Step 4: Check Password and Account Status

VPN login may fail if:

- Password expired
- Password was changed recently
- Account is locked
- Account is disabled
- User is not in the VPN security group
- MFA is not registered
- User is using an old saved password

If Active Directory is used, check account status and group membership.

Example group:

```text
VPN-Users
```

## Step 5: Check MFA

Many VPNs require multi-factor authentication.

Check:

- User received MFA prompt
- User approved the correct prompt
- Phone has internet access
- Authenticator app is working
- User did not deny or ignore the prompt
- Device time is correct

Escalate if MFA needs re-registration or reset.

## Step 6: Connect VPN and Check IP Configuration

After VPN connects, run:

```cmd
ipconfig /all
```

Check for:

- VPN adapter
- VPN IP address
- DNS servers
- Connection suffix
- Default gateway or routes

If VPN connects but internal resources do not work, DNS or routing may be the issue.

## Step 7: Test Internal Resources

Test internal server by name:

```cmd
ping fileserver01
nslookup fileserver01.company.local
```

Test by IP address, if known:

```cmd
ping 192.168.10.20
```

Troubleshooting logic:

```text
Can reach internal IP but not internal name = possible DNS issue.
Cannot reach internal IP or name = possible VPN routing or access issue.
```

## Step 8: Test Shared Drives

Example shared drive path:

```text
\\FileServer01\Shared
```

If shared drive does not open:

- Confirm VPN is connected
- Confirm internal DNS works
- Confirm user has permissions
- Confirm mapped drive uses correct path
- Disconnect and reconnect mapped drive if needed

## Step 9: Check Saved Credentials

Old saved credentials can break VPN or shared drive access.

Check Credential Manager:

```cmd
control keymgr.dll
```

Look for old saved credentials related to:

- VPN
- File server
- Microsoft 365
- Internal applications
- Domain account

Remove or update only if approved.

## Step 10: Restart VPN Client and Computer

If the VPN client is stuck:

1. Disconnect VPN.
2. Close VPN client.
3. Reopen VPN client.
4. Try again.
5. Restart computer if needed.

## Step 11: Check VPN Split Tunnel vs Full Tunnel

Some VPNs route all traffic through the company network. Others only route internal traffic through VPN.

Issues may happen if:

- Internal traffic is not routed through VPN
- DNS uses public servers instead of internal DNS
- Local network subnet conflicts with company subnet
- Firewall blocks VPN traffic

These issues may require escalation.

## Useful Commands

### Check IP configuration

```cmd
ipconfig /all
```

### Flush DNS

```cmd
ipconfig /flushdns
```

### Test internet

```cmd
ping 8.8.8.8
ping google.com
```

### Test internal DNS

```cmd
nslookup fileserver01.company.local
```

### Test internal server

```cmd
ping fileserver01
ping 192.168.10.20
```

### Open Credential Manager

```cmd
control keymgr.dll
```

### View route table

```cmd
route print
```

## Common VPN Issues and Fixes

| Issue | Possible Cause | Resolution |
|---|---|---|
| VPN will not connect | Wrong password or account locked | Verify identity and check account |
| MFA prompt missing | MFA app or registration issue | Confirm MFA device and escalate if needed |
| VPN connects but shared drive fails | DNS or permission issue | Test DNS and shared path |
| VPN connects but internal IP fails | Routing issue | Check VPN routes and escalate |
| VPN disconnects often | Unstable internet | Test local network connection |
| New password not working | Cached old credentials | Update saved credentials |
| User not authorized | Missing VPN group | Add user to approved VPN group if authorized |

## Escalation Criteria

Escalate if:

- Multiple users cannot connect to VPN
- VPN server may be down
- MFA reset is required
- VPN certificate is expired
- User is missing required access approval
- Routing issue is suspected
- VPN client requires reinstallation
- Security incident is suspected

## Example Ticket Note

```text
User reported VPN connected but shared drive was unavailable.
Confirmed internet access was working before VPN connection.
User connected VPN successfully.
Ran ipconfig /all and confirmed VPN adapter was active.
Nslookup for fileserver01 failed, indicating internal DNS issue.
User disconnected and reconnected VPN, then received correct DNS server.
Confirmed \\FileServer01\Shared opened successfully.
Ticket resolved.
```

## Security Considerations

VPN access should be handled carefully because it allows remote access to company systems.

Best practices:

- Verify user identity before account changes
- Do not bypass MFA
- Do not share passwords
- Confirm user is authorized for VPN access
- Report suspicious login activity
- Escalate repeated authentication failures
- Follow company remote access policy

## Skills Demonstrated

- VPN troubleshooting
- Remote user support
- DNS and routing awareness
- MFA support awareness
- Credential Manager basics
- Network command-line diagnostics
- Security-focused support documentation
