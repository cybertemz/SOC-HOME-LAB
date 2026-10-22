# Tools in My SOC Home Lab

## VMware Workstation Pro 17

VMware Workstation lets me run Ubuntu Server and Windows 10 as virtual machines on my Windows computer. It gives me a place to practise configuration and troubleshooting without installing those operating systems directly on the host.

I plan to keep snapshots before major changes and check the VM's memory, disk and network settings when troubleshooting.

## Ubuntu Server 24.04.1 LTS

Ubuntu is the Linux machine I use for command-line practice and SSH. These commands help me check the system:

    hostnamectl
    ip -br addr
    whoami

They show the hostname and operating-system details, network addresses and current user.

## PowerShell and OpenSSH

I use Windows PowerShell to connect to Ubuntu over SSH:

    ssh <ubuntu-username>@<ubuntu-lab-ip>

SSH encrypts the remote session. The host key helps identify the server, while user authentication checks whether the account is allowed to connect. The connection to my Ubuntu shell worked during my test.

## Windows 10 endpoint

The Windows VM is the endpoint I use to practise monitoring. Windows records different kinds of activity in event logs, but those events only become useful for central investigation when the right log sources are configured and collected.

I use Event Viewer to inspect local logs and the Wazuh dashboard to check the agent and search for collected data.

## Sysmon

Sysmon records detailed Windows activity in the Sysmon Operational event log. The exact events recorded depend on its configuration. In my lab, I have viewed Sysmon events locally; I still need to document a matching event in Wazuh to verify the full collection path.

## Wazuh

Wazuh is the SIEM I'm learning to use. The agent collects configured data from an endpoint, the manager processes incoming events, and the dashboard lets me search events and review alerts.

The dashboard is accessible, and the Windows agent has appeared as Active. My next step is to find a specific event in the dashboard and inspect any related alert.

## Remote Desktop Protocol (RDP)

RDP is used for interactive access to a Windows desktop. In my test, I reached the credentials prompt, but I have not yet recorded evidence that the desktop session opened and accepted input. I will only mark RDP as working after that check.

## Keeping the lab safe

- Do not commit passwords, SSH private keys, Wazuh enrollment secrets or API tokens.
- Use unique passwords for lab accounts.
- Keep remote administration and monitoring services on the intended lab network.
- If a secret is accidentally published, rotate it; deleting it from the latest file does not remove it from Git history.
