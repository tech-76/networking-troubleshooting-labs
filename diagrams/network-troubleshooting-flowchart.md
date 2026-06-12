# Network Troubleshooting Flowchart

## Purpose

This diagram shows a professional help desk workflow for troubleshooting network connectivity issues. It separates the process into intake, scope identification, local device checks, IP/DHCP checks, gateway testing, internet connectivity, DNS troubleshooting, application testing, and escalation.

```mermaid
flowchart LR
    A["User reports<br/>network issue"] --> B["Confirm issue details<br/>error message, device, location"]
    B --> C{"Scope of issue?"}

    C -->|One user| D["Local device troubleshooting"]
    C -->|Multiple users| Z1["Check for wider outage<br/>network, ISP, firewall, switch, Wi-Fi"]

    subgraph S1["Step 1: Local Device Checks"]
        D --> E["Check Wi-Fi or Ethernet<br/>connection status"]
        E --> F["Restart affected app<br/>or browser"]
        F --> G["Check network adapter<br/>enabled / connected"]
    end

    subgraph S2["Step 2: IP and DHCP Checks"]
        G --> H["Check IP configuration<br/>ipconfig /all"]
        H --> I{"Valid IP address?"}
        I -->|No| J["Renew DHCP lease<br/>or reconnect network"]
        J --> H
        I -->|Yes| K["Confirm subnet, gateway,<br/>and DNS settings"]
    end

    subgraph S3["Step 3: Gateway and LAN Testing"]
        K --> L["Ping default gateway"]
        L --> M{"Gateway reachable?"}
        M -->|No| N["Check local network<br/>cable, Wi-Fi, adapter, VLAN"]
        M -->|Yes| O["LAN path appears working"]
    end

    subgraph S4["Step 4: Internet Connectivity Testing"]
        O --> P["Ping public IP<br/>example: 8.8.8.8"]
        P --> Q{"Public IP reachable?"}
        Q -->|No| R["Check router, firewall,<br/>ISP, VPN, or upstream path"]
        Q -->|Yes| S["Internet path appears working"]
    end

    subgraph S5["Step 5: DNS and Application Testing"]
        S --> T["Test DNS resolution<br/>nslookup / Resolve-DnsName"]
        T --> U{"DNS working?"}
        U -->|No| V["Check DNS settings,<br/>DNS server, or DNS cache"]
        U -->|Yes| W["Test website or application"]
        W --> X{"Application works?"}
    end

    X -->|Yes| Y["Resolve ticket<br/>document fix and user confirmation"]
    X -->|No| AA["Escalate with notes<br/>commands, results, screenshots"]

    Z1 --> Z2["Check service status<br/>and network alerts"]
    Z2 --> Z3["Escalate to network<br/>or system admin team"]

    R --> AA
    V --> AA
    N --> AA

    classDef start fill:#1f2937,stroke:#111827,color:#ffffff,stroke-width:2px;
    classDef process fill:#dbeafe,stroke:#2563eb,color:#111827,stroke-width:1px;
    classDef decision fill:#fef3c7,stroke:#d97706,color:#111827,stroke-width:1px;
    classDef issue fill:#fee2e2,stroke:#dc2626,color:#111827,stroke-width:1px;
    classDef success fill:#dcfce7,stroke:#16a34a,color:#111827,stroke-width:1px;
    classDef escalate fill:#ede9fe,stroke:#7c3aed,color:#111827,stroke-width:1px;

    class A start;
    class B,D,E,F,G,H,J,K,L,O,P,S,T,W,Z1,Z2 process;
    class C,I,M,Q,U,X decision;
    class N,R,V issue;
    class Y success;
    class AA,Z3 escalate;
```

## What This Diagram Demonstrates

* Network issue intake
* One-user vs multiple-user troubleshooting
* Local device troubleshooting
* IP address and DHCP checks
* Default gateway testing
* Internet connectivity testing
* DNS troubleshooting
* Website and application testing
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
