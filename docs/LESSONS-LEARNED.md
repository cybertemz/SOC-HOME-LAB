# What I've Learned So Far

## Take one step at a time

I built the lab in stages: installing Ubuntu, connecting over SSH, creating the Windows VM, trying RDP and accessing Wazuh. Checking each stage separately makes it easier to see where a problem starts.

## Remote access and monitoring are different

A working SSH session means I can reach the Ubuntu shell through that connection. It doesn't mean Wazuh is collecting events. In the same way, reaching the RDP credentials prompt doesn't prove that a remote desktop session has opened.

Each part needs its own test.

## Dashboard access is only the beginning

I learned that being able to open the Wazuh dashboard is not enough to prove that the full monitoring setup works. I also need a connected agent, configured event collection, searchable event data and evidence for any detection I describe.

## Keep notes tied to evidence

When I document a step, I want to record what I did, what result I saw and what still needs checking. Screenshots help, but the caption should explain what is visible instead of claiming more than the image proves.

## What I want to do next

- Confirm the VMware network mode I'm using.
- Finish testing RDP.
- Check the Wazuh component and service status.
- Find a harmless Windows or Sysmon event in Wazuh.
- Review a related alert if one is generated and explain what it means.
- Keep the project README updated as I verify each stage.

I'm still learning, and I want this repository to show that process honestly rather than make the lab look more complete than it is.
