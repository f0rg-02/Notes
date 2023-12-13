---
Name: tcpdump
Platform: Linux
tags: Resources
---
`tcpdump` is a command line packet sniffer. Is in all Linux repos on Distros I've used.

Can be used to isolate traffic, limit the size of file, sniff specific ports, can be used in scripts like bash.

Install: 

```
sudo apt install tcpdump
```

Basic usage:

```
tcpdump -i <interface>
```

Write to PCAP:

```
tcpdump -i <interface> -w whatever.pcap 
```

To not do DNS resolution and just show as IP addresses:

```
tcpdump -i <interface> -n
```

------

Can save to pcap file and use tools like [[PCredz]], [[dsniff]], [[Brute Shark]], etc. for offline analysis.