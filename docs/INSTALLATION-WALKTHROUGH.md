# SOC Home Lab — Installation Walkthrough and Evidence Plan

This guide explains the purpose of each stage, what I did, why I did it, and what the evidence proves. The goal is to show a repeatable learning process—not a gallery of unrelated screenshots.

## How to read this lab

Each project follows the same order:

1. **Objective** — what I wanted to achieve.
2. **Why it matters** — how the task fits into a small SOC environment.
3. **What I did** — the practical work performed.
4. **Verification** — what the available evidence actually demonstrates.
5. **Evidence** — only the clearest screenshots, with a caption explaining why each one matters.
6. **Limitations / next step** — anything not yet demonstrated.

Screenshots should support the explanation, not replace it. Keep around two or three useful images per project. Do not upload duplicate screens, installer pages that add no new information, passwords, tokens, private keys, or credential prompts with visible details.

---

## 1. Virtual environment — VMware Workstation

### Objective
Prepare a virtualisation platform so I can run isolated operating systems for hands-on cybersecurity practice without installing every system directly on my host computer.

### Why I did this
A SOC lab needs separate machines that can act as endpoints and servers. VMware lets me create and manage these virtual machines, allocate resources, and practise in a controlled environment.

### What I did
I worked through the VMware Workstation Pro setup and used it to create/start a Windows 10 virtual machine. The screenshots supplied show the VMware setup wizard and the Windows desktop running in a VM.

### What I understand
VMware is the virtualisation layer; it is not the operating system or the SIEM. It provides the virtual hardware on which guest operating systems run. A working Windows desktop is evidence that the guest boots, but it does not prove that networking or remote access is configured.

### Keep as evidence
- **VMware setup screen:** use only if you need to demonstrate the platform/setup stage.
- **Windows 10 desktop running in VMware:** strongest evidence that a guest VM started.

Avoid uploading several nearly identical installer wizard screens. If the repository already documents the VM successfully, the desktop screenshot alone may be enough.

---

## 2. Ubuntu Server installation — Linux lab machine

### Objective
Set up an Ubuntu Server virtual machine to practise Linux administration and provide a system that I can manage remotely.

### Why I did this
Linux servers are common in technical environments. Learning to install and inspect Ubuntu builds the foundation for using SSH and later hosting or managing security tools.

### What I did
I used the Ubuntu Server installer in VMware and worked through the installation and initial system setup. The supplied screenshots show the installer and terminal output from the Ubuntu environment.

### What I understand
Ubuntu Server is the guest operating system. After installation, I need to verify that it boots, has a network address, and can be administered. The installer screen alone is not proof of successful networking or remote access.

### Verification to record
Use the VM console to confirm that Ubuntu reaches a login/shell prompt. To check its current address, run:

```bash
ip -br addr
```

Only add command output as evidence if it was actually captured and the result is readable.

### Keep as evidence
- One clear screenshot of the Ubuntu installation/first successful boot.
- One readable terminal screenshot showing the system is available, if present.

Do not upload every page of the installer.

---

## 3. SSH remote access — Windows host to Ubuntu VM

### Objective
Connect to Ubuntu from Windows PowerShell over SSH, without needing to interact with the Ubuntu VM console for every command.

### Why I did this
SSH is a standard way to administer Linux servers remotely. This exercise demonstrates a useful host-to-guest management workflow and prepares me to manage Linux systems from a Windows workstation.

### What I did
From Windows PowerShell, I used the SSH client to connect to the Ubuntu VM using its current private lab address and Ubuntu username:

```powershell
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

The actual username and address should be substituted locally. The VM address can change, so I should check it before reconnecting.

### What I understand
SSH provides an authenticated remote shell. Reaching the Ubuntu shell prompt confirms that the SSH connection worked at the time of the test. It does not mean Remote Desktop (RDP) is working; SSH and RDP are different protocols for different purposes.

### Keep as evidence
- **Connection established:** PowerShell showing the SSH command and Ubuntu shell prompt.
- **Optional supporting check:** a clear screenshot showing the session and a basic command executed inside Ubuntu.

Do not publish passwords, private keys, or unnecessary network details.

---

## 4. Windows 10 Remote Desktop — RDP test

### Objective
Test the Remote Desktop Connection workflow toward the Windows lab machine.

### Why I did this
RDP is used to access a Windows desktop remotely. It is a separate capability from SSH and requires the target Windows edition, settings, network reachability, and credentials to be configured correctly.

### What I did
The supplied screenshots show Remote Desktop Connection and a Windows Security credentials prompt for the target private lab address.

### What I understand
Reaching a credentials prompt shows that the connection workflow progressed to authentication, but it does **not** by itself prove that a usable remote desktop session opened. I should only mark RDP as complete after I successfully sign in and see/control the remote desktop.

### Keep as evidence
- One screenshot of the RDP connection attempt or credentials stage, with sensitive information hidden.
- If later successful, replace or supplement it with one screenshot of the actual remote Windows desktop.

Never publish passwords or screenshots that expose credentials.

---

## 5. Wazuh SIEM installation and dashboard access

### Objective
Set up and access Wazuh, a security monitoring platform used to collect and analyse endpoint telemetry and display security-related events and alerts.

### Why I did this
A SIEM helps an analyst bring security data into one place for investigation. Installing or opening the dashboard is only the platform setup stage; monitoring needs a connected endpoint and evidence that data is arriving.

### What I did
The supplied Wazuh archive contains screenshots of the Wazuh website/documentation and dashboard interface. Those images can show the official platform reference and dashboard access, but they do not clearly prove every central component installed successfully.

### What I understand
The central Wazuh components have separate responsibilities:
- **Manager/server:** receives and analyses agent data.
- **Indexer:** stores and indexes data.
- **Dashboard:** interface used to search and review information.
- **Agent:** software installed on an endpoint to collect configured data.

I must not claim that event collection or detection works end to end just because the dashboard opens. For the central installation, I still need clear command/service evidence if I want to document installation success.

### Keep as evidence
- One screenshot showing the dashboard successfully loaded.
- One screenshot showing the installation result or relevant service status, **only if the result is clearly visible**.

The supplied images of the Wazuh public website are background/reference images and are not strong evidence of a successful installation. Prefer actual terminal or dashboard evidence.

### Security
Do not upload the generated Wazuh admin password, password archives, tokens, or other secrets. Keep the dashboard on the intended lab network.

---

## 6. Wazuh agent deployment on Windows

### Objective
Enroll the Windows 10 VM as an endpoint monitored by the Wazuh manager.

### Why I did this
The central Wazuh platform cannot monitor this Windows endpoint until an agent is installed/configured and communicating with the manager. The agent is the bridge that sends configured endpoint information to Wazuh.

### What I did
The existing project notes record running the agent installation from an elevated PowerShell session, starting the Wazuh service, testing TCP connectivity, and seeing the endpoint listed as **Active** in the Wazuh dashboard.

### What I understand
These checks answer different questions:
- A successful installer/service message indicates the Windows agent service was installed or started.
- A successful TCP test proves only that the specific network test succeeded at that time.
- **Active** in the dashboard is evidence that the manager sees the agent as active.
- None of these alone proves that a particular Windows event generated a detection alert.

### Keep as evidence
Use no more than these three screenshots:
1. **Installation/service start** — PowerShell output showing the service started successfully.
2. **Connectivity check** — readable output showing the actual test and its successful result.
3. **Active endpoint** — Wazuh Endpoints view showing the Windows agent and its status.

The dashboard overview can be omitted if the Active endpoint screenshot already proves the milestone. Do not include duplicate screenshots just to increase the image count.

### Next validation
Generate a harmless test event, find it in Wazuh, and document the search result. If a detection alert is created, record its timestamp, rule ID, and severity. Until then, describe the agent deployment as verified but event-to-alert detection as not yet demonstrated.

---

## Screenshot naming and captions

Use descriptive filenames instead of camera-generated names, for example:

- `01-vmware-windows-vm-running.png`
- `01-ubuntu-installation-or-first-boot.png`
- `02-ssh-from-windows-to-ubuntu.png`
- `03-rdp-credentials-prompt-redacted.png`
- `04-wazuh-dashboard-access.png`
- `05-wazuh-agent-service-started.png`
- `06-wazuh-agent-active.png`

For every image, add a one-sentence caption that states what is visible and what that evidence proves. Do not imply that an image proves more than it shows.

## Publishing checklist

- [ ] Keep the repository's existing root README and documentation; add to them rather than replacing the project.
- [ ] Keep one clear README per project or one linked documentation page per stage.
- [ ] Limit each stage to the strongest two or three screenshots.
- [ ] Use relative image paths so screenshots display inside GitHub.
- [ ] Check that each image is readable on GitHub's web view.
- [ ] Redact credentials and remove any secret files before publishing.
- [ ] Separate verified results from future work.
