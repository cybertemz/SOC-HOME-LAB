# SSH Authentication Log Monitoring and Investigation

## What I tested

I wanted to see what happens in Wazuh when someone makes unsuccessful SSH login attempts against my Ubuntu endpoint. From a separate device in my own lab, I made repeated SSH login attempts using an incorrect password. I did this as a controlled test so I could see whether the Ubuntu system recorded the activity and whether it appeared in Wazuh.

## What I checked in Wazuh

In the Wazuh **Discover** page, I selected the `wazuh-archives*` index and filtered the events for the `ubuntu-agent` endpoint. I narrowed the search to the authentication events and reviewed the matching records.

The screenshot shows **2 matching events** in the selected time range. In the event details, the `full_log` field contains an SSH/PAM message reporting additional authentication failures. This is the evidence I used to confirm that the failed login activity was being recorded and was searchable in Wazuh.

![Wazuh Discover showing SSH authentication failure logs for the Ubuntu agent](../Screenshot%202026-11-05%20054022.png)

## What the result tells me

The test showed me how failed SSH logins can be investigated from a central dashboard instead of checking the endpoint log manually each time. The useful details include the agent name, event timestamp, decoder, and the original log message.

A few failed logins do not automatically prove that a brute-force attack is taking place. In this lab, I generated the attempts deliberately from a second device. In a real environment, I would look at the source address, number and frequency of failures, usernames being tried, whether a successful login followed, and any other activity from the same source before deciding how serious it is.

## Investigation steps I followed

1. Generated repeated unsuccessful SSH login attempts from a separate device in my lab.
2. Opened Wazuh Discover and selected the archive events.
3. Filtered the results to the Ubuntu agent.
4. Reviewed the authentication records and opened the event details.
5. Checked the timestamp and original `full_log` message to understand what the event represented.

## What I learned

This exercise helped me connect an action on an endpoint with the logs collected by a SIEM. I also got more practice filtering events and reading the original log message instead of relying only on the event count.

My next step is to run a longer controlled test and compare the event timestamps and source details. I also want to check whether the activity triggers a Wazuh alert under the rules enabled in my lab. The screenshot in this note is evidence of searchable authentication-failure events; it is not, by itself, evidence that Wazuh raised a brute-force alert.

## Lab safety

I carried out this test only against my own Ubuntu virtual machine in my private lab. I did not test against public systems or devices I do not own or have permission to assess.
