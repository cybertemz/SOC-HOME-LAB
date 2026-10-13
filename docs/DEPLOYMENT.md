# Deployment Journal
## Setup Steps and Verification Record

This guide distinguishes actions recorded as completed from items that still require verification. Commands are examples for the described lab and may need adjustment for the current VM network and configuration.

## Phase 1 — Create the Virtual Lab

### Ubuntu Server
1. Create a virtual machine in VMware Workstation Pro 17.
2. Attach the Ubuntu Server 24.04.1 LTS ISO.
3. Complete the OS installation.
4. Configure the hostname and a local username/password.
5. Enable OpenSSH Server during installation or install it afterward.
6. Boot the VM and confirm it reaches a login prompt.

**Recorded status:** Ubuntu Server installed.

### Windows 10
1. Create a Windows 10 VM using the VMware wizard.
2. Configure its virtual disk and basic VM settings.
3. Start the VM and confirm the Windows desktop loads.

**Recorded status:** VM created and desktop startup verified.

## Phase 2 — Verify Ubuntu Network and SSH

### Find the guest address

Run inside Ubuntu:

```bash
ip -br addr
```

Use the active interface address on the lab network. Do not assume an old DHCP address remains the same after a reboot.

### Connect from Windows PowerShell

```powershell
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

On first connection, compare the displayed host fingerprint with a trusted value when possible. Continue only if the host identity is expected. Then authenticate with the Ubuntu account.

**Recorded verification:** The SSH session reached the Ubuntu welcome message and shell prompt.

### Optional service checks

On Ubuntu:

```bash
sudo systemctl status ssh
sudo ss -lntp | grep ':22'
```

These commands are checks to use if SSH stops working; the current notes do not record their output.

## Phase 3 — Initiate Windows Remote Desktop

On the Windows system, run:

```powershell
ipconfig
```

Use the relevant lab interface address, then open **Remote Desktop Connection** and enter the target VM address. Complete the Windows Security prompt using an authorized account.

**Recorded status:** The connection workflow reached the credential prompt.  
**Pending verification:** Confirm that authentication succeeds, the remote desktop opens, and mouse/keyboard control works.

If the session fails, check that the target VM is running, RDP is enabled, the account is permitted to sign in through Remote Desktop, and the lab network/firewall allows the connection.

## Phase 4 — Wazuh Dashboard Access

1. Review the official Wazuh installation documentation.
2. Access the Wazuh dashboard.
3. Record where the manager, indexer, and dashboard components are installed.
4. Confirm the relevant services are healthy.
5. Enroll the Windows endpoint using the appropriate Wazuh agent procedure.
6. Verify the endpoint status and generate a harmless test event.
7. Search for the event and record the evidence.

**Recorded status:** Dashboard accessed.  
**Pending verification:** Component health, agent enrollment, event ingestion, and alert validation.

Official documentation: https://documentation.wazuh.com/

## Phase 5 — End-to-End Verification Checklist

- [ ] Ubuntu guest has a current lab-network address.
- [x] SSH from Windows PowerShell reaches an Ubuntu shell.
- [x] Windows 10 VM desktop startup was checked.
- [ ] RDP opens a usable remote desktop session.
- [ ] Wazuh manager/indexer/dashboard topology is documented.
- [ ] Windows endpoint appears active in Wazuh.
- [ ] A controlled Windows event is searchable in Wazuh.
- [ ] A detection rule produces an expected alert from a safe test.
- [ ] The test, timestamp, query, result, and limitations are documented.

Checkboxes represent the state in the available project notes, not an automatic live check of the machines.
