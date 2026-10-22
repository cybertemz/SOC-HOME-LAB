# My SOC Home Lab

## Project overview

I built this home lab to understand how a Security Operations Center (SOC) collects endpoint activity, brings it into one place, and helps an analyst investigate events. Rather than treating security tools as separate installations, I wanted to understand the role each component plays in a monitoring workflow.

This is a hands-on learning project running in VMware Workstation. I use a dedicated Ubuntu VM as my Wazuh server, a Windows 10 Pro VM as an endpoint, and a separate Ubuntu VM with the Wazuh agent deployed. My Windows endpoint also has Sysmon installed.

## What I understand about SOC monitoring

A SOC analyst needs visibility into activity across computers, a way to search and correlate events, and a process for deciding which activity needs investigation. A SIEM such as Wazuh centralizes security events and can generate alerts when collected data matches configured rules. An alert is a lead to investigate, not automatic proof that an attack has occurred.

In this lab, I am learning to distinguish between three different things:

- **Generating telemetry:** a system or tool records activity.
- **Collecting and centralizing logs:** an agent forwards configured logs to the monitoring platform.
- **Investigating detections:** an analyst reviews the event details, context, and any matching alert before drawing a conclusion.

Seeing an agent marked **Active** in the Wazuh dashboard confirms that it is connected to the manager. By itself, that status does not prove that every expected log source is configured or that a particular event has arrived.

## How Wazuh and Sysmon fit together

### Wazuh server

My dedicated Ubuntu server hosts the Wazuh monitoring platform. The Wazuh manager receives events from enrolled agents, analyzes supported data using decoders and rules, and produces alerts when activity matches detection logic. The Wazuh dashboard provides a place to review agent status, search available data, and investigate alerts.

I verified that the `wazuh-manager` service on my server showed **active (running)**. The dashboard also showed my Windows and Ubuntu agents as **Active**.

**Evidence — Wazuh Manager service**

![Wazuh Manager service status](./wazuhmanager%20status.png)

This terminal output supports the claim that the manager service was running when I checked it.

### Wazuh agent

I deployed Wazuh agents to my Windows 10 endpoint and my separate Ubuntu endpoint. The agents provide a way for the server to receive supported endpoint information. What reaches Wazuh depends on the agent configuration, available log sources, and the event collection settings.

**Evidence — endpoint connectivity**

![Wazuh dashboard showing active Windows and Ubuntu agents](./wazuhagentdashboard.png)

The dashboard shows both agents as Active. This confirms connection status, not by itself the successful arrival of every type of event.

### Sysmon on Windows

Sysmon (System Monitor) is a Windows system service and driver that records detailed system activity in the Windows Event Log. It provides useful telemetry for investigating what happened on an endpoint. Sysmon does not, by itself, decide that an event is malicious, and recording an event is not the same as generating a Wazuh alert.

Depending on the Sysmon configuration, event types can include:

- **Event ID 1 — Process creation:** records a process starting, including useful context such as the image and command line when configured.
- **Event ID 3 — Network connection:** records network connections made by a process when network-connection logging is enabled.
- **Event ID 7 — Image loaded:** records a module or image loaded by a process when enabled; this can be high-volume.
- **Event IDs 12, 13 and 14 — Registry events:** record selected registry key/object creation or deletion, value setting, and key/value renaming activity, depending on the event ID and configuration.

The events collected depend on Sysmon's configuration, so this list describes common event types rather than claiming that every event type is enabled in my lab. My Event Viewer screenshot shows the Sysmon Operational log populated with events, including visible examples of process, image-load, registry, and network-related activity.

**Evidence — Sysmon Operational log on Windows**

![Sysmon Operational events in Windows Event Viewer](./windows%20sysmonevent.png)

This screenshot shows locally recorded Sysmon events on my Windows endpoint.

### How Sysmon events can reach the Wazuh dashboard

The intended event path is:

1. Sysmon records selected Windows activity in **Microsoft-Windows-Sysmon/Operational**.
2. The Wazuh agent on Windows must be configured to collect that Sysmon event channel.
3. The agent forwards collected events to the Wazuh server.
4. Wazuh processes the incoming data. Depending on the event, configuration, and matching rules, it may be searchable in the dashboard and may produce an alert.
5. A SOC analyst reviews the event details and surrounding context to decide whether further investigation is needed.

**Verification note:** My screenshots currently demonstrate that Sysmon has recorded local Windows events and that the Windows and Ubuntu agents appear Active in Wazuh. I have not included a screenshot that independently proves a specific Sysmon event was received and searched in Wazuh. I will claim end-to-end Sysmon forwarding only after I verify it in the dashboard.

**Evidence — Ubuntu agent status**

![Ubuntu Wazuh agent status evidence](./wazuhagentstatus.png)

Use this image as agent-service evidence only if it shows the Ubuntu agent service status; otherwise, replace it with a direct screenshot of `sudo systemctl status wazuh-agent` on the `ubuntuagent` VM.

## Lab architecture

| Component | Role in my lab |
|---|---|
| Windows host computer | Runs the virtual machines |
| VMware Workstation | Provides the isolated lab environment |
| Ubuntu Wazuh server | Central monitoring and analysis |
| Windows 10 Pro VM | Endpoint with Wazuh agent and Sysmon |
| Separate Ubuntu VM | Endpoint monitored by its Wazuh agent |
| Wazuh dashboard | Agent visibility, event search, and alert investigation |
| Windows Event Viewer | Local inspection of Sysmon Operational events |

## Evidence approach

The screenshots embedded above are intended to sit beside the explanation they support. They are real captures from my lab, not simulated or AI-generated results. I will keep each caption specific to what the image actually proves.

## What I learned and what I will test next

Building this lab has helped me understand that a monitoring setup is more than installing a SIEM. The server, agents, event sources, and collection configuration each have a different job. A healthy agent connection is an important first check, while useful detection work also depends on confirming that the right events are collected and then investigating their meaning.

My next validation steps are to:

1. Confirm that the Windows Wazuh agent is configured to collect the Sysmon Operational channel.
2. Generate or identify a benign test event and locate the matching event in Wazuh.
3. Check whether the event produces an alert, and explain why it did or did not.
4. Record the result with a real screenshot and document any configuration changes.

This is a learning lab, not a production SOC. I will continue to separate verified results from work that still needs testing.

## Security and documentation habits

- I do not publish passwords, private keys, or generated credentials.
- I avoid exposing SSH, RDP, or the Wazuh dashboard directly to the public internet.
- I review screenshots for sensitive details before publishing them.
- I document what I tested, what the evidence shows, and what remains unverified.

## Related project notes

- [Project overview](docs/PROJECT-OVERVIEW.md)
- [Deployment notes](docs/DEPLOYMENT.md)
- [Wazuh agent deployment](docs/WAZUH-AGENT-DEPLOYMENT.md)
- [Wazuh installation notes](docs/WAZUH-INSTALLATION.md)
- [Architecture](docs/ARCHITECTURE.md)
- [Components](docs/COMPONENTS.md)
- [Troubleshooting](docs/TROUBLESHOOTING.md)
- [Lessons learned](docs/LESSONS-LEARNED.md)
