# Wazuh Installation Notes

## Why I'm using Wazuh

Wazuh is the SIEM and security-monitoring platform I'm using in my SOC home lab. I want to understand how endpoint information is collected, processed and made available for investigation.

I'm keeping installation and service checks separate from endpoint monitoring tests, because opening the dashboard alone doesn't prove that events are reaching it.

## Environment

| Item | Details |
|---|---|
| Host | Windows computer |
| Virtualisation | VMware Workstation Pro 17 |
| Linux VM | Ubuntu Server 24.04.1 LTS |
| Monitoring platform | Wazuh |

The official [Wazuh Quickstart guide](https://documentation.wazuh.com/current/quickstart.html) is my reference for the installation process.

## Main components

- **Wazuh manager:** receives and analyses data from enrolled agents.
- **Wazuh indexer:** stores and indexes events and alerts.
- **Wazuh dashboard:** provides the interface for reviewing data.
- **Wazuh agent:** runs on an endpoint and collects the sources configured for that machine.

The server-side components and the endpoint agent each have a different role. I need to check their status and then test event collection separately.

## Progress recorded so far

I have accessed the Wazuh dashboard and worked on deploying the Windows agent. My Windows agent deployment notes contain the evidence for the service start and the endpoint appearing as Active.

I have not recorded enough evidence in this document to confirm the exact installed Wazuh version, the location of every central component, or a complete event-to-alert test. I won't mark those items as completed until I check them.

## Checks to complete

- [ ] Record the Wazuh version and the installation method used.
- [ ] Confirm where the manager, indexer and dashboard are running.
- [ ] Check the relevant service status.
- [ ] Confirm that the dashboard is accessible after the service checks.
- [ ] Confirm endpoint enrollment and agent status.
- [ ] Find a harmless test event in the dashboard before claiming event collection works.
- [ ] Validate an alert only after the event has been located and its details reviewed.

## Lab security

I keep Wazuh and remote administration services on the intended lab network. I do not commit passwords, generated credentials, API tokens or private keys. I also review screenshots before publishing them.

## Current takeaway

I can access the dashboard and have evidence of the Windows agent showing as Active. The next important milestone is to verify a specific endpoint event in Wazuh and record what I find.
