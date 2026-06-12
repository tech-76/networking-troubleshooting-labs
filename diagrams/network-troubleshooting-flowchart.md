# Network Troubleshooting Flowchart

## Purpose

This diagram shows a clear help desk workflow for troubleshooting network connectivity issues. It is designed to be readable on GitHub without needing to zoom in.

```mermaid
flowchart TB
    A["User Reports Network Issue"] --> B["Confirm Issue Details<br/>Device, location, error message, connection type"]
    B --> C{"Is the issue affecting<br/>one user or multiple users?"}

    C -->|One user| D["Start Local Device Troubleshooting"]
    C -->|Multiple users| Z1["Check for Wider Network Issue<br/>Possible outage, switch, firewall, Wi-Fi, ISP, or service issue"]

    D --> E["Check Connection Type<br/>Wi-Fi, Ethernet, or VPN"]
    E --> F["Confirm Physical or Wireless Connection<br/>Cable connected, Wi-Fi joined, VPN connected"]
    F --> G["Restart Browser, App, or Device<br/>Confirm issue still happens"]

    G --> H["Check IP Configuration<br/>Use ipconfig /all or Get-NetIPConfiguration"]
    H --> I{"Does the device have<br/>a valid IP address?"}

    I -->|No| J["Renew IP Address<br/>ipconfig /release<br/>ipconfig /renew<br/>Reconnect network"]
    J --> H

    I -->|Yes| K["Check Default Gateway<br/>Confirm gateway is listed"]
    K --> L["Ping Default Gateway"]
    L --> M{"Is the gateway<br/>reachable?"}

    M -->|No| N["Local Network Issue<br/>Check cable, Wi-Fi signal, adapter, VLAN, or access point"]
    M -->|Yes| O["Test Internet Path<br/>Ping public IP such as 8.8.8.8"]

    O --> P{"Can the device reach<br/>a public IP address?"}

    P -->|No| Q["Upstream Connectivity Issue<br/>Check router, firewall, ISP, VPN, or routing"]
    P -->|Yes| R["Test DNS Resolution<br/>Use nslookup or Resolve-DnsName"]

    R --> S{"Is DNS working?"}

    S -->|No| T["DNS Issue<br/>Check DNS server, DNS settings, DNS cache, or domain resolution"]
    S -->|Yes| U["Test Website or Application<br/>Confirm if the original service now works"]

    U --> V{"Is the issue resolved?"}

    V -->|Yes| W["Resolve Ticket<br/>Document fix, commands used, and user confirmation"]
    V -->|No| X["Escalate Ticket<br/>Include troubleshooting notes, screenshots, command results, and impact"]

    Z1 --> Z2["Check Network Alerts or Service Status"]
    Z2 --> Z3["Escalate to Network or System Administrator Team"]

    N --> X
    Q --> X
    T --> X

    classDef start fill:#1f2937,stroke:#111827,color:#ffffff,stroke-width:2px;
    classDef process fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:1px;
    classDef decision fill:#fef3c7,stroke:#d97706,color:#111827,stroke-width:1px;
    classDef issue fill:#fee2e2,stroke:#dc2626,color:#111827,stroke-width:1px;
    classDef success fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:1px;
    classDef escalate fill:#ede9fe,stroke:#7c3aed,color:#111827,stroke-width:1px;

    class A start;
    class B,D,E,F,G,H,J,K,L,O,R,U,Z1,Z2 process;
    class C,I,M,P,S,V decision;
    class N,Q,T issue;
    class W success;
    class X,Z3 escalate;
```

## What This Diagram Demonstrates

* Help desk network troubleshooting workflow
* Single-user versus multiple-user issue checking
* Wi-Fi, Ethernet, and VPN troubleshooting
* IP address and DHCP troubleshooting
* Default gateway testing
* Internet connectivity testing
* DNS troubleshooting
* Application testing
* Escalation documentation

## Common Windows Commands

```powershell
ipconfig /all
ipconfig /release
ipconfig /renew
ping 127.0.0.1
ping 8.8.8.8
ping google.com
nslookup google.com
tracert google.com
```

## Common PowerShell Commands

```powershell
Get-NetIPConfiguration
Test-Connection 8.8.8.8
Resolve-DnsName microsoft.com
Get-DnsClientServerAddress
```

## Example Help Desk Scenarios

| Scenario                                              | First Area to Check                       |
| ----------------------------------------------------- | ----------------------------------------- |
| User cannot access any websites                       | IP configuration and DNS                  |
| User is connected to Wi-Fi but internet does not work | Gateway and DNS checks                    |
| One laptop has no connection                          | Local device and adapter checks           |
| Multiple users cannot connect                         | Wider network or outage check             |
| User can ping IP but not domain names                 | DNS troubleshooting                       |
| VPN user cannot reach internal resources              | VPN, routing, DNS, and permissions        |
| Application works for others but not one user         | Local profile, browser, app, or DNS cache |

## Escalation Notes to Include

When escalating the ticket, include:

* User impact
* Device name
* Network type: Wi-Fi, Ethernet, or VPN
* Error messages
* IP address status
* Gateway ping result
* Public IP ping result
* DNS test result
* Application or website tested
* Screenshots if available
* Troubleshooting already completed

## Portfolio Note

This diagram is part of a networking troubleshooting lab designed to demonstrate IT Support, Help Desk, Desktop Support, and Junior Systems Administrator troubleshooting workflows.
