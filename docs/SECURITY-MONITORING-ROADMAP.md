# Security Monitoring Roadmap
## From a Working Lab to Verified SIEM Telemetry

This roadmap describes the next steps. It is not evidence that these integrations have already been completed.

## Milestone 1 — Confirm the Wazuh Deployment

Record:
- Wazuh version.
- Where manager, indexer, and dashboard components run.
- Service health.
- Lab addresses (use placeholders in public notes).
- Required endpoint-to-manager connectivity for the installed version.

Do not copy passwords or enrollment secrets into the documentation.

## Milestone 2 — Onboard the Windows Endpoint

1. Confirm the Windows 10 VM has network connectivity to the Wazuh manager.
2. Install the Wazuh agent using the official instructions appropriate for the installed version.
3. Configure the manager address using the lab's actual topology.
4. Start the agent and complete enrollment.
5. Confirm the endpoint appears active in the dashboard.
6. Record the verification time and any relevant non-sensitive status output.

Official documentation: https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-windows.html

## Milestone 3 — Verify Event Collection

Use a harmless test that generates a normal Windows event, such as a controlled sign-in or a benign process launch. Follow local lab policy and avoid testing against systems outside the lab.

Record:
- What event was generated and why.
- Timestamp and endpoint.
- Which event source/channel should contain it.
- Search filters used in Wazuh.
- Whether the event appeared and how long it took.
- Any limitations or missing fields.

Do not create a suspicious payload just to test the pipeline. The goal is to verify collection safely.

## Milestone 4 — Validate a Detection

After collection is proven:
1. Choose a built-in Wazuh rule relevant to the test event.
2. Confirm the rule logic and expected severity.
3. Run a benign test that should match the rule, if available.
4. Verify the resulting alert and record the rule ID, timestamp, endpoint, and evidence.
5. Document false positives and tuning needs.

Do not label a rule as operational until the expected alert has been reproduced and reviewed.

## Milestone 5 — Add Linux Telemetry (Optional)

Once the Windows path is stable, consider enrolling Ubuntu as another monitored endpoint. Verify agent connectivity and a test event separately from Windows so that issues can be isolated by source.

## Milestone 6 — Document an Investigation

For a validated alert, capture a small incident record:
- Summary and timeline.
- Affected lab endpoint.
- Observed evidence and relevant event fields.
- Hypothesis and validation steps.
- Containment/remediation performed, if any.
- Final outcome and lessons learned.

## Definition of Done

The monitoring milestone is complete only when the endpoint is active, a test event is searchable, and the documented detection produces the expected alert. A dashboard login alone does not meet this definition.
