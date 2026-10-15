# KB-002 — Windows Network and DNS Troubleshooting

A step-by-step check for a Windows PC that can't reach the internet or a specific website. Everything here runs from Command Prompt.

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

Replies mean the PC can reach the internet by IP address. No replies doesn't always mean an outage, because some networks block ICMP.

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

Record the commands, their output, and when you ran them in the ticket.

Escalate if the fix needs changes to a router, DNS server, firewall, or the ISP connection.

## Example: NSIT-3

When I ran these steps for [NSIT-3](../tickets/NSIT-3-network-troubleshooting.md), everything passed:

| Test | Result |
|---|---|
| IPv4 address | 192.168.40.36 |
| Default gateway / DNS server | 192.168.40.1 |
| `ping 1.1.1.1` | 4/4 replies, 0% loss |
| `nslookup microsoft.com` | Resolved to 150.171.110.211 |
| `tracert microsoft.com` | Destination reached at hop 16 |

A clean result like this rules out a general connectivity or DNS failure on the tested machine. It doesn't prove the user's specific problem is fixed.
