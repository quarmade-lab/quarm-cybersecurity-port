# KB-002 — Windows Network and DNS Troubleshooting

## Purpose

Provide a repeatable troubleshooting process for Windows workstations experiencing internet connectivity or DNS resolution issues.

## Tools

- Windows Command Prompt
- ipconfig
- ping
- nslookup
- tracert
- Jira Service Management

## Procedure

### Step 1 — Confirm the Issue

Ask the employee:

- Which website or service is affected?
- What exact error message appears?
- Does the issue affect other websites?
- When did the problem begin?
- Are other employees affected?

### Step 2 — Check Network Configuration

Open Command Prompt and run:

```cmd
ipconfig /all
```

Review the IPv4 address, subnet mask, default gateway, DNS servers, and DHCP configuration.

### Step 3 — Test IP Connectivity

Run:

```cmd
ping 1.1.1.1
```

Review packet loss and response times.

Successful replies demonstrate ICMP connectivity to the tested destination. Failed replies do not always establish a network outage because ICMP may be blocked.

### Step 4 — Test DNS Resolution

Run:

```cmd
nslookup microsoft.com
```

Check whether the DNS server returns an address.

If DNS resolution fails while external IP connectivity succeeds, investigate DNS configuration and server availability.

### Step 5 — Trace the Network Route

Run:

```cmd
tracert microsoft.com
```

Review the visible network hops and whether the destination responds.

Intermediate timeouts do not necessarily indicate a routing failure.

### Step 6 — Document and Escalate

Record commands, timestamps, actual outputs, and affected services.

Escalate when the issue requires router, DNS server, firewall, ISP, or infrastructure changes outside the technician's authority.

## Lab Findings — NSIT-3

| Test | Observed Result |
|---|---|
| IPv4 address | 192.168.40.3 |
| Default gateway | 192.168.40.1 |
| DNS server | 192.168.40.1 |
| Ping 1.1.1.1 | 0% packet loss |
| DNS lookup | microsoft.com resolved successfully |
| Traceroute | Destination reached at hop 16 |

These results demonstrate successful tests on the lab workstation, not resolution of a fictional employee's incident.

## Related Lab

[NSIT-3 — Network Troubleshooting](../tickets/NSIT-3-network-troubleshooting.md)

---

*Prepared for a simulated IT support environment.*
