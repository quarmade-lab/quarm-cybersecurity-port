# Lessons Learned

## What worked

- **Doing the admin work in PowerShell.** Every step left a command and its output on screen, which made it easy to document and repeat.
- **Checking after every change.** `Stop-Service` and `Start-Service` return nothing when they succeed. Running `Get-Service` after each one was the only proof the change happened.
- **Using one resource group for the whole lab.** Deleting `RG-ServerLab` removed all six resources in one step, with nothing left to track down.

## What I'd do differently

- **Check prompts before moving on.** My first `Read-Host` password prompt was submitted empty. I cancelled the next command before it created the account, but it's an easy mistake to miss.
- **Tie the logs to the outage.** I reviewed the System log but didn't filter it. Next time I'd filter for Event ID 7036 around the time of the Spooler stop and start, so the log entries line up with the incident.
- **Lock down RDP.** RDP was open only for the lab, but for anything longer I'd restrict the inbound rule to my own IP address.
- **Capture the cleanup result.** I have a screenshot of the resource group before deletion, not after. A screenshot of the empty list would close the loop.
- **Think about VM size.** Memory was at 72% on a 4 GiB VM with only admin tools open. That's fine for a short lab but worth knowing before putting a workload on a VM that size.

## Takeaways for support work

- A stopped service is quick to confirm and fix from PowerShell, but the fix only counts once the status is checked again.
- Azure metrics and in-VM tools answer different questions. One shows the VM from the outside without signing in; the other shows which processes are responsible.
