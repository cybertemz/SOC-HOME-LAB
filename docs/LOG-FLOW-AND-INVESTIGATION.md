# Log Flow and Investigation Workflow

## Lab overview

My lab uses VMware Workstation with three virtual machines:

- **WAZUHSERVER** — the Ubuntu VM hosting the Wazuh server components.
- **Windows 10 Pro** — an endpoint with the Wazuh Agent and Sysmon installed.
- **ubuntuagent** — a separate Ubuntu endpoint with the Wazuh Agent deployed.

The Wazuh dashboard screenshot shows the Windows and Ubuntu agents as Active. On the server, I checked `sudo systemctl status wazuh-manager` and observed the manager service as active (running).

## Expected event path

```text
Windows 10 endpoint
  Sysmon
    -> Windows Event Log: Microsoft-Windows-Sysmon/Operational
      -> Wazuh Agent (when the channel is configured)
        -> Wazuh server / manager
          -> Wazuh dashboard: search events and review alerts

Ubuntu endpoint
  Ubuntu system logs
    -> Wazuh Agent
      -> Wazuh server / manager
        -> Wazuh dashboard: review collected data and alerts
```

This diagram describes the intended collection workflow. The Windows Sysmon-to-Wazuh path still needs a specific end-to-end event check before I claim that forwarding is verified.

## How I would investigate an event

1. Identify what the event records and which host produced it.
2. Check its timestamp, process or user context, and other available fields.
3. Search related events around the same time to build context.
4. Review whether Wazuh generated an alert and which rule matched it, if any.
5. Decide whether the activity is expected, suspicious, or requires more evidence.
6. Record the finding and the evidence. Avoid calling an event malicious based on a single field alone.

## What my current evidence establishes

- Wazuh Manager: the service status screenshot shows `active (running)`.
- Agent connectivity: the Wazuh dashboard shows the Windows and Ubuntu agents as Active.
- Local Sysmon logging: the Windows Event Viewer screenshot shows Sysmon Operational events.

## What remains to verify

- Confirm that the Windows Wazuh Agent configuration includes the Sysmon Operational event channel.
- Find a specific Sysmon event in Wazuh after it is generated on Windows.
- Determine whether the event creates an alert or is only available as searchable event data.
- Capture a direct screenshot of that Wazuh event and document the result.

## Security note

These VMs are for an isolated learning lab. I avoid publishing passwords, tokens, private keys, or unnecessary network details. Screenshots should be checked for sensitive information before sharing.
