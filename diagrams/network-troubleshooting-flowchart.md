# Network Troubleshooting Flowchart

## Purpose

This flowchart shows a basic IT support and help desk workflow for troubleshooting network connectivity issues.

```mermaid
flowchart TD
    A["User reports network issue"] --> B["Confirm issue details"]
    B --> C{"One user or multiple users affected?"}

    C -->|One user| D["Check local device"]
    C -->|Multiple users| E["Check wider network or outage"]

    D --> F["Check Wi-Fi or Ethernet connection"]
    F --> G["Check IP configuration"]
    G --> H{"Valid IP address?"}

    H -->|No| I["Renew DHCP or reconnect network"]
    H -->|Yes| J["Ping default gateway"]

    J --> K{"Gateway reachable?"}
    K -->|No| L["Check local network, cable, Wi-Fi, adapter"]
    K -->|Yes| M["Ping public IP address"]

    M --> N{"Public IP reachable?"}
    N -->|No| O["Check router, firewall, ISP, VPN"]
    N -->|Yes| P["Test DNS resolution"]

    P --> Q{"DNS working?"}
    Q -->|No| R["Check DNS settings or DNS server"]
    Q -->|Yes| S["Test website or application"]

    S --> T{"Application works?"}
    T -->|Yes| U["Resolve ticket and document fix"]
    T -->|No| V["Escalate with troubleshooting notes"]

    E --> W["Check service status or network outage"]
    W --> X["Escalate to network/system admin team"]
```

## What This Diagram Demonstrates

- Basic network troubleshooting workflow
- Single-user vs multi-user issue checking
- DHCP and IP troubleshooting
- Gateway testing
- Public connectivity testing
- DNS troubleshooting
- Escalation process
- Help desk documentation workflow

## Common Commands

### Windows Commands

```powershell
ipconfig /all
ping 8.8.8.8
ping google.com
nslookup google.com
tracert google.com
```

### PowerShell Commands

```powershell
Get-NetIPConfiguration
Test-Connection 8.8.8.8
Resolve-DnsName microsoft.com
```

## Example Use Cases

- User cannot browse the internet
- User can connect to Wi-Fi but websites do not load
- DNS issue affecting one workstation
- Possible DHCP issue
- Local adapter or cable problem
- VPN-related connectivity issue
- Wider network outage requiring escalation
