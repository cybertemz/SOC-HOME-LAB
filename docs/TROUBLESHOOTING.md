# Troubleshooting
## Checks for Common Home-Lab Problems

Start with the lowest layer and change one thing at a time: VM state, network address, reachability, service status, authentication, then application or SIEM state.

## 1. Ubuntu SSH Connection Fails

### Check the guest is running and has an address
Inside Ubuntu:

```bash
ip -br addr
```

Confirm the address belongs to the expected VMware interface and use the current address rather than an old DHCP lease.

### Check SSH service
```bash
sudo systemctl status ssh
sudo ss -lntp | grep ':22'
```

If the service is inactive, inspect the service output before making changes. On Ubuntu, the service is commonly named `ssh`.

### Check from PowerShell
```powershell
Test-NetConnection <ubuntu-lab-ip> -Port 22
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

If the TCP test fails, check VM networking and firewall rules. If the TCP test succeeds but authentication fails, check the username, account state, and configured authentication method.

### Host fingerprint warning
A host-key change can occur after a VM is rebuilt, but it can also indicate that the target is not the expected machine. Verify the fingerprint through a trusted path before removing or replacing a saved host key.

## 2. RDP Does Not Open a Desktop

Check:
- The Windows target VM is running and has a current address.
- Remote Desktop is enabled on the target edition and configuration.
- The user is allowed to sign in through Remote Desktop.
- Windows Firewall permits RDP from the intended lab network.
- The client is connecting to the correct target address.

Reaching the credentials prompt is only partial progress. Confirm the desktop opens and accepts input before marking the connection complete.

## 3. Wazuh Dashboard Opens but No Endpoint Events Appear

A dashboard login does not prove ingestion. Check in order:
1. The Wazuh manager, indexer, and dashboard services are healthy.
2. The Windows endpoint can reach the configured manager.
3. The Wazuh agent is installed, running, and enrolled.
4. The endpoint appears active in the dashboard.
5. The selected time range and query match the test event.
6. The relevant event collection settings are enabled.

Record exact errors and timestamps, but redact tokens, passwords, and private details before sharing logs.

## 4. VMware Network Address Changes

A guest address can change when DHCP leases renew or the VM network configuration changes. Re-check `ip -br addr` in Ubuntu or `ipconfig` in Windows before troubleshooting a remote connection.

Document the network mode (NAT, host-only, or bridged) and use the right interface for the intended path.

## 5. Safe Troubleshooting Practice

- Take a snapshot before risky configuration changes.
- Capture the current state before restarting services.
- Avoid disabling firewalls as a first-line fix.
- Never expose SSH, RDP, or Wazuh services publicly just to make connectivity work.
- Remove secrets and sensitive host details from pasted logs.
