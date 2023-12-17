---
Name: p0f
Platform: Linux
tags: Resources
---
Passive OS Fingerprint and Network Analysis. Useful over nmap or something like that because it doesn't send active probes like Nmap does or an active network sniffer does.

Install:

```Ruby
sudo apt install p0f
```

------

Basic Usage:

```Ruby

Sniff with interface:
p0f -i eth0 -p -o /tmp/p0f.log

Read a pcap file and output to a log file:
p0f -r <path to pcap file> -o /tmp/p0f.log
```

------

Passive is useful to stay less noisy.