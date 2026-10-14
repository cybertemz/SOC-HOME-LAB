# My SOC Home Lab

I'm building this lab to learn the practical side of cybersecurity. So far, I've set up Ubuntu Server and Windows 10 in VMware, connected to Ubuntu over SSH from PowerShell, and deployed a Wazuh agent to my Windows VM.

I'm documenting what I actually did, including the checks I ran and what the screenshots show. This is a learning lab, not a production SOC.

## What I've done

- Installed Ubuntu Server 24.04.1 LTS in VMware Workstation.
- Connected from Windows PowerShell to Ubuntu using SSH and reached the Linux shell.
- Created a Windows 10 virtual machine and checked that the desktop started.
- Opened the Wazuh dashboard.
- Installed the Wazuh agent on Windows, started its service, tested connectivity, and saw the endpoint listed as **Active** in Wazuh.

The agent deployment is documented, but I haven't yet documented a specific Windows event being found in Wazuh and matched to a detection alert. I also haven't confirmed that an RDP session opens to a usable desktop.

## My setup

| Part | What I'm using |
|---|---|
| Host | Windows computer |
| Virtualization | VMware Workstation Pro 17 |
| Linux VM | Ubuntu Server 24.04.1 LTS |
| Windows VM | Windows 10 Pro |
| Remote shell | PowerShell SSH client and OpenSSH |
| Security monitoring | Wazuh dashboard and Windows agent |

## Project notes

- [Project overview](docs/PROJECT-OVERVIEW.md) — what I built and where the lab stands.
- [Deployment notes](docs/DEPLOYMENT.md) — Ubuntu, SSH, Windows VM, and initial Wazuh work.
- [Wazuh agent deployment](docs/WAZUH-AGENT-DEPLOYMENT.md) — the Windows agent steps and evidence from my screenshots.
- [Wazuh installation notes](docs/WAZUH-INSTALLATION.md) — initial Wazuh setup and what still needs checking.
- [Architecture](docs/ARCHITECTURE.md) — how the parts of the lab fit together.
- [Components](docs/COMPONENTS.md) — the tools and what I used them for.
- [Troubleshooting](docs/TROUBLESHOOTING.md) — useful checks for issues in the lab.
- [Lessons learned](docs/LESSONS-LEARNED.md) — notes from working through the setup.

## What I want to test next

My next monitoring exercise is to generate a harmless Windows event, find it in Wazuh, and then check whether a relevant alert is created. I'll add that result only after I test it.

## A few lab habits

- I keep passwords, private keys, and generated credentials out of GitHub.
- I avoid exposing SSH, RDP, or the Wazuh dashboard directly to the public internet.
- I try to separate what I've verified from what I still need to test.
- I use screenshots as evidence and will redact sensitive details before publishing them.

This lab is a work in progress. I'm learning by building, troubleshooting, and documenting one step at a time.
