# Troubleshooting Notes

When something stops working, I check one layer at a time: the VM, its IP address, network reachability, service status, authentication, and finally the application.

## Ubuntu SSH connection fails

First, check that Ubuntu is running and has a current IP address:

    ip -br addr

Then check the SSH service and whether anything is listening on port 22:

    sudo systemctl status ssh
    sudo ss -lntp | grep ':22'

From PowerShell, I can test the connection and try SSH again:

    Test-NetConnection <ubuntu-lab-ip> -Port 22
    ssh <ubuntu-username>@<ubuntu-lab-ip>

If the TCP test fails, I check the VM network mode and firewall rules. If the TCP test works but login fails, I check the username, account and authentication method.

If SSH warns that the host key has changed, I verify that I'm connecting to the correct VM before changing the saved host key. A rebuilt VM can have a new key, but the warning should not be ignored automatically.

## RDP does not open the Windows desktop

I check that the Windows VM is running, that I'm using its current address, that Remote Desktop is enabled, and that the account is allowed to connect. I also check that the firewall allows the connection from the lab network.

Reaching the credentials prompt is only partial progress. I need to see and control the remote desktop before I call the connection successful.

## Wazuh dashboard opens but I cannot find events

Opening the dashboard is not the same as confirming event collection. I check:

1. Whether the relevant Wazuh services are running.
2. Whether the endpoint can reach the configured manager.
3. Whether the agent is installed, running and enrolled.
4. Whether the endpoint appears Active.
5. Whether the search and time range match the event I am looking for.
6. Whether the required event channel or log source is enabled in the agent configuration.

I keep the exact error and timestamp when troubleshooting, but remove passwords, tokens and other sensitive details before sharing logs.

## A VM's IP address changes

A DHCP address can change after a lease renews or the network configuration changes. I check the current address in Ubuntu or Windows before trying an old one.

## Safe troubleshooting habits

- Take a snapshot before risky changes.
- Check the current state before restarting services.
- Avoid turning off the firewall as a first fix.
- Do not expose SSH, RDP or Wazuh directly to the public internet to solve a lab connection problem.
- Remove secrets from screenshots and copied logs.
