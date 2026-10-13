# Lessons Learned
## Notes from Building the SOC Home Lab

## 1. Verify Before Expanding

The lab was built in stages: Ubuntu installation, SSH access, Windows VM creation, RDP initiation, and Wazuh dashboard access. Keeping the stages separate makes it easier to identify which layer needs attention.

## 2. Remote Access and Monitoring Are Different

A successful SSH session proves that remote administration works for that path. It does not prove that system events are collected by a SIEM. Similarly, reaching the RDP credential prompt does not prove that the desktop session succeeds.

Each workflow needs its own success criteria.

## 3. A Dashboard Is Not the Same as an End-to-End SIEM

Accessing the Wazuh dashboard confirms initial access to the interface. A functioning monitoring pipeline also requires healthy backend components, an enrolled agent, event transmission, searchable events, and validated detections.

## 4. Document the Evidence

For each milestone, keep a concise record of:
- What was configured.
- The exact command or UI path used, with secrets omitted.
- The expected result.
- The actual result.
- Any unresolved issue.
- The next step.

Screenshots can help, but they should be cropped or redacted to avoid publishing credentials, tokens, private addresses, or other sensitive information.

## 5. Improvements to Make Next

- Confirm and document the VMware network mode.
- Finish RDP verification.
- Record the Wazuh component topology and service health.
- Enroll the Windows endpoint and validate a test event.
- Build a small, evidence-based detection exercise.
- Add an incident investigation example after event collection is working.
- Keep the README status table synchronized with verified progress.
