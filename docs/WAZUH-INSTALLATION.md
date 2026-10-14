# Wazuh Installation and Initial Access
## SOC Home Lab — Installation Record

## 1. Objective

This stage documents the Wazuh setup work for the SOC home lab. Wazuh is a security monitoring platform used to collect endpoint telemetry, analyse events, and present security alerts.

This record distinguishes initial installation/dashboard access from a fully verified monitoring pipeline.

## 2. Lab Environment

| Item | Recorded environment |
|---|---|
| Host | Windows computer |
| Virtualization | VMware Workstation Pro 17 |
| Linux VM | Ubuntu Server 24.04.1 LTS |
| Platform | Wazuh |
| Official reference | [Wazuh Quickstart](https://documentation.wazuh.com/current/quickstart.html) |

Record the exact Wazuh version and component placement from the installation output rather than assuming them.

## 3. Main Components

- **Wazuh server:** receives and analyses data from enrolled agents.
- **Wazuh indexer:** stores and indexes security events and alerts.
- **Wazuh dashboard:** web interface for reviewing events and alerts.
- **Wazuh agent:** endpoint software that collects configured data and sends it to the Wazuh server.

The central components and the endpoint agent have different roles. Dashboard access alone does not prove that endpoint monitoring is working.

## 4. Installation Approach

The official Wazuh documentation provides installation instructions and an installation assistant for deploying the central components. Use the official guide appropriate to the actual deployment.

**Command evidence:** Add the exact command used from the installation screenshots or notes after confirming it. Do not invent a command or claim a successful result without supporting output.

Official reference: [Wazuh Quickstart](https://documentation.wazuh.com/current/quickstart.html).

## 5. Recorded Progress

| Checkpoint | Status in current project notes |
|---|---|
| Official Wazuh documentation reviewed | Recorded |
| Wazuh dashboard accessed | Recorded |
| Exact version and component topology | Needs confirmation |
| Manager, indexer, and dashboard service health | Needs verification |
| Windows agent enrolled and active | Not verified in this record |
| Test event searchable in the dashboard | Not verified |
| Detection alert validated end to end | Not verified |

These statuses must be updated only when there is evidence from the installation output, service checks, or dashboard.

## 6. Screenshots and Evidence

Add the existing installation screenshots to this section after confirming their filenames and contents. Suggested captions, only where supported by the image:

1. **Installation process** — command or installer progress.
2. **Installation result** — final installer status or result.
3. **Initial dashboard access** — Wazuh interface visible.

Before uploading, remove or obscure passwords, generated credentials, tokens, private keys, and other sensitive information. Do not describe an installer as successful unless the screenshot actually shows a successful result.

## 7. Verification Checklist

- [ ] Record the installed Wazuh version and actual installation method.
- [ ] Identify where the server, indexer, and dashboard components are running.
- [ ] Check and record the relevant service status.
- [ ] Confirm dashboard access after checking the services.
- [ ] Treat Windows agent enrollment as a separate milestone.
- [ ] Generate a harmless test event and confirm it is searchable before claiming event collection works.
- [ ] Validate a detection only after the event pipeline is confirmed.

## 8. Security and Lab Hygiene

- Keep Wazuh and remote-administration services on the intended lab network.
- Do not expose the dashboard, SSH, or RDP directly to the public internet.
- Never commit passwords or generated Wazuh credentials.
- Redact sensitive details in screenshots and logs.
- Make one configuration change at a time and record the observed result.

## 9. Outcome

This document records the Wazuh setup stage and the initial dashboard access noted for the SOC home lab. Full SIEM operation remains **unverified** until service health, agent enrollment, event ingestion, and detection validation have been demonstrated and documented.

---

*Project method: verify the evidence, document the actual result, and distinguish completed work from the next milestone.*
