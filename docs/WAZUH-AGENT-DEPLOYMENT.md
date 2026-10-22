# Wazuh Agent Deployment on Windows 10

## Why I deployed the agent

I installed the Wazuh agent on my Windows 10 Pro virtual machine so the endpoint could send configured information to my Wazuh environment for monitoring. This is part of my practice lab, where I'm learning how endpoint data gets from a computer into a SIEM.

## Lab details

| Item | Value shown in my notes or screenshots |
|---|---|
| Virtualisation | VMware Workstation |
| Windows endpoint | Windows 10 Pro |
| Wazuh server address | 192.168.239.134 |
| Agent name | wazuhwindows10 |
| Agent ID | 001 |
| Agent group | default |

The IP address is a private lab address and may change if the virtual network uses DHCP.

## What I did

### 1. Created the agent deployment command

In the Wazuh dashboard, I opened **Endpoints** and selected **Deploy new agent**. I selected the Windows package and used the manager address and agent name for this lab.

Wazuh's official instructions are available in the [Windows agent deployment guide](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html).

### 2. Ran the installer

I ran the generated installation command in an Administrator PowerShell window. The command was configured to point the Windows agent at my Wazuh server.

### 3. Started the service

I ran:

    NET START Wazuh

The terminal returned **“The Wazuh service was started successfully.”** This confirms that the Windows service started during that test.

### 4. Checked connectivity

One of my screenshots shows a TCP test returning TcpTestSucceeded: True for port 1515. That records a successful test to that port at that moment. It is not, by itself, proof that all agent communication is working, so I also checked the agent status in the dashboard.

### 5. Checked the dashboard

The Wazuh Endpoints view showed:

- Agent ID: 001
- Agent name: wazuhwindows10
- Operating system: Windows 10 Pro
- Group: default
- Status: **Active**

This is the main evidence I have that the Windows endpoint was registered and connected when I took the screenshot.

## What the evidence tells me

The screenshots support that I ran the agent installer, started the Wazuh service, completed the displayed TCP test, and saw the endpoint listed as Active. They do not yet show a specific Windows or Sysmon event being found in Wazuh.

## Next checks

- [ ] Generate a harmless Windows event and search for it in Wazuh.
- [ ] Record the event time, search used and result.
- [ ] If an alert appears, record its rule ID and severity.
- [ ] Recheck the agent status after a later refresh.
- [ ] Keep the relevant screenshots in the repository with captions that explain what each one shows.

## Conclusion

The Windows agent deployment is a step toward central monitoring, but it is not the end of the test. My next goal is to follow one event from the Windows endpoint into Wazuh and document the result.
