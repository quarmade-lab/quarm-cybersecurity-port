# Troubleshooting: Print Spooler Outage

This was a simulated outage on a lab server. I stopped the service myself to practise the detect, fix, and verify steps. No printers or users depended on it.

## Summary

| Field | Detail |
|---|---|
| Server | `Quarm-Server01` |
| Service | Print Spooler (`Spooler`) |
| Symptom | Service stopped (simulated) |
| Cause | Stopped on purpose with `Stop-Service` |
| Fix | Started the service with `Start-Service` |
| Status | Resolved and verified `Running` |

## Baseline

Before simulating anything, I checked the service and restarted it once to make sure it stopped and started cleanly:

```powershell
Get-Service Spooler       # Status: Running
Restart-Service Spooler
```

## 1. Simulate the outage

```powershell
Stop-Service Spooler
```

## 2. Identify the stopped service

```powershell
Get-Service Spooler
```

Result: `Stopped   Spooler   Print Spooler`. In a real ticket, this is where "I can't print" turns into a confirmed cause on the server.

## 3. Restore the service with PowerShell

```powershell
Start-Service Spooler
```

## 4. Verify normal operation

```powershell
Get-Service Spooler
```

Result: `Running   Spooler   Print Spooler`. The service was back in its normal state.

![Print Spooler running, stopped, then running again](../screenshots/service-troubleshooting.png)

## Notes

- `Stop-Service` and `Start-Service` don't print anything when they work, so the `Get-Service` check after each one is what proves the change.
- Since I caused the outage, there was no root cause to find. In a real case, the next step would be checking the System log for why the service stopped and whether it keeps happening.
