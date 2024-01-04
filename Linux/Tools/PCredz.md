---
Name: PCreds
Platform: Linux
tags: Resources
---
Extracts credentials on a number of protocols either from PCAP or live interface.

Install on Debian:

```
apt install python3-pip && sudo apt-get install libpcap-dev && pip3 install Cython && pip3 install python-libpcap
```

------

Usage:

```
# extract credentials from a pcap file
python3 ./Pcredz -f file-to-parse.pcap

# extract credentials from all pcap files in a folder
python3 ./Pcredz -d /tmp/pcap-directory-to-parse/

# extract credentials from a live packet capture on a network interface (need root privileges)
python3 ./Pcredz -i eth0 -v
```

Very simple and useful. Reminds me of [[p0f]] and [[dsniff]]
