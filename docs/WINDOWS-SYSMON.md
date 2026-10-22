# Windows Sysmon — Telemetry and Investigation Notes

## Purpose

I installed Sysmon on my Windows 10 Pro VM to gain more detailed visibility into activity on the endpoint. Windows logs provide important operating-system and security records; Sysmon adds selected low-level telemetry that can help an analyst understand what a process did and what activity occurred around it.

Sysmon records events. It does not independently determine that every recorded action is malicious, and an event is not automatically a security alert.

## Event types I am learning to interpret

Sysmon event collection depends on the active configuration. Common event IDs include:

| Event ID | Event type | Why an analyst may care |
|---|---|---|
| 1 | Process creation | Helps investigate which executable started, its command line, parent process, and related context. |
| 3 | Network connection | Can help associate network activity with a process. This event type must be enabled in the Sysmon configuration. |
| 7 | Image loaded | Shows DLL/image loading; it can be high-volume and is configuration-dependent. |
| 12 | Registry object create/delete | Helps investigate selected registry key/object changes. |
| 13 | Registry value set | Can help investigate changes to registry values, including some persistence-related activity. |
| 14 | Registry key/value rename | Adds context about selected registry renaming activity. |

These are examples of event types, not a claim that every possible Sysmon event is enabled in my lab. My Event Viewer screenshot shows that the Sysmon Operational log contains recorded events, including visible examples of network, process, image-load, and registry activity.

## How the data is intended to reach Wazuh

1. Sysmon records selected activity in the Windows Event Log channel `Microsoft-Windows-Sysmon/Operational`.
2. The Wazuh Agent on Windows must be configured to read that event channel.
3. The agent forwards collected events to the Wazuh server.
4. Wazuh processes the event data. Depending on parsing, rules, and configuration, an event may be searchable and may or may not create an alert.
5. An analyst reviews the event details, checks surrounding context, and decides whether further investigation is warranted.

## Evidence and validation status

My screenshots show Sysmon Operational events locally and show the Windows endpoint as Active in the Wazuh dashboard. An Active agent status confirms agent connectivity, but does not prove that the Sysmon channel is configured for collection or that a specific Sysmon event reached Wazuh.

My next validation task is to search for a known benign Sysmon event in Wazuh and capture evidence of the event arriving. I will update this section once that end-to-end check is completed.

## Lessons learned

- Endpoint telemetry, log forwarding, and alert generation are separate stages.
- A high event count is not the same as detection quality.
- Sysmon configuration affects which event types are recorded and the volume of data.
- I should document only what I can verify in my own lab.
