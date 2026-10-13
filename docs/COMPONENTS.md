# Components and Remote Access
## Purpose, Operation, and Security Notes

## 1. VMware Workstation Pro 17

VMware Workstation runs the Ubuntu Server and Windows 10 virtual machines on the host computer. It provides a controlled environment for testing without installing the guest operating systems directly on the host.

**Operational notes**
- Use clear VM names and take snapshots before major changes.
- Record CPU, RAM, disk, and network settings as the lab evolves.
- Prefer a private or NAT network for routine practice; use bridged mode only when you understand the exposure it creates.

## 2. Ubuntu Server 24.04.1 LTS

Ubuntu Server is the Linux guest used for command-line administration and SSH practice. The initial installation included creation of a hostname and local account.

Useful commands:

```bash
hostnamectl
ip -br addr
whoami
```

These commands show the system identity, interface addresses, and active user. Avoid publishing account names or private addresses if they reveal unnecessary lab details.

## 3. OpenSSH Server

OpenSSH provides encrypted remote shell access. In this lab, Windows PowerShell is the client and Ubuntu Server is the SSH host.

```powershell
ssh <ubuntu-username>@<ubuntu-lab-ip>
```

### Authentication concepts
- **Host key/fingerprint:** helps the client verify that it is connecting to the expected server.
- **User authentication:** proves that the connecting user is authorized, for example with the configured account credentials or an SSH key.
- **Encryption:** protects the SSH session in transit after negotiation.

The recorded setup used the Ubuntu account credentials and accepted a host fingerprint prompt. The notes do not establish whether public-key authentication is configured, whether password authentication remains enabled, or what the effective SSH daemon policy is.

If checking configuration, use:

```bash
sudo sshd -T | grep -E 'passwordauthentication|pubkeyauthentication|permitrootlogin'
```

Treat the output as a current configuration check, not as a value already verified by this repository.

## 4. Windows 10 Endpoint VM

The Windows guest is intended to produce endpoint telemetry for security monitoring exercises. Windows can record sign-ins, process activity, service changes, and other system events, but the lab still needs a verified collection path before those events can be investigated centrally.

Potential verification tools:
- Event Viewer for inspecting local event channels.
- PowerShell for querying event logs.
- Wazuh agent status and endpoint state after onboarding.

## 5. Remote Desktop Protocol (RDP)

RDP provides interactive remote access to a Windows desktop. The recorded workflow checked network configuration with `ipconfig`, opened Remote Desktop Connection, entered the target address, and reached the credential prompt.

A successful prompt is not proof that the session opened. Record the outcome after confirming that the desktop is visible and controllable. Restrict RDP to the lab network and authorized users.

## 6. Wazuh SIEM

Wazuh is the intended security-monitoring platform. The dashboard was accessed, but the current documentation does not yet confirm a working endpoint-to-dashboard pipeline.

The next evidence should include:
- Where Wazuh manager, indexer, and dashboard are running.
- Agent installation/enrollment status.
- Endpoint last-seen/active status.
- A harmless generated event and the matching event in the dashboard.
- A validated alert, with rule details and timestamp.

## 7. Credentials and Secrets

- Do not place account passwords, SSH private keys, Wazuh enrollment secrets, API tokens, or recovery codes in this repository.
- Use unique passwords for lab accounts.
- Prefer SSH keys for ongoing administration once the workflow is understood and tested.
- Keep SIEM and remote administration services on the private lab network.
- If a secret is accidentally committed, rotate it; deleting it from the latest file does not remove it from Git history.
