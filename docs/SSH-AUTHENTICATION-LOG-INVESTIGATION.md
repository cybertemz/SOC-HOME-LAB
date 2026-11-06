# SSH Authentication Log Monitoring and Investigation

## What I tested

I wanted to check whether Wazuh would record failed SSH logins on my Ubuntu endpoint and make those events easy to find. I used a second device in my lab to make repeated SSH login attempts with an incorrect password. This was a controlled, brute-force-style test against my own VM, not a test against somebody else's system.

## What I checked in Wazuh

After the test, I opened **Discover** in the Wazuh dashboard, selected the `wazuh-archives*` index, and filtered the results for `ubuntu-agent` and authentication activity.

The screenshot shows **2 matching events** in the selected time range. I opened the event details and checked the agent information, SSH decoder, and original log message. The `full_log` field contains a PAM message reporting additional authentication failures. That gave me evidence that the failed login activity from my test was reaching the Ubuntu logs and was searchable in Wazuh.

![Wazuh Discover showing Linux SSH authentication log events](../LINUX%20Log%20Monitoring.png)

## What the result tells me

This exercise helped me follow an activity from a separate device through to the logs collected from my Ubuntu endpoint. Instead of relying only on the terminal, I could use Wazuh Discover to filter the records and inspect the original message.

The two matching events and the PAM message are evidence of authentication failures. They do not, on their own, prove that a real attacker carried out a brute-force attack or that Wazuh generated a brute-force alert. For a proper investigation, I would also check the source IP, the usernames being attempted, the timing and frequency of the failures, whether any login succeeded afterwards, and whether a Wazuh alert was generated.

## Steps I followed

1. Used a second device in my lab to make repeated unsuccessful SSH login attempts against my Ubuntu VM.
2. Opened Wazuh Discover and selected the archive events.
3. Filtered the results for the Ubuntu agent and authentication activity.
4. Opened the matching records and reviewed the agent, decoder, timestamp, and original log message.
5. Used the event details to confirm what the records were reporting.

## What I learned

I got a better understanding of how Linux authentication activity can be collected and reviewed centrally. I also practised filtering events in Wazuh and reading the original log message instead of making a decision based only on the event count.

My next step is to repeat the test while recording the source address and timing, then check whether the rules enabled in my lab generate an alert for that pattern. I will keep the difference clear between an event being collected and an alert being triggered.

## Lab safety

I performed this test only against my own Ubuntu virtual machine in my private lab, using a second device I control. I did not target public systems or devices I do not have permission to test.
