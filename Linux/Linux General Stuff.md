# Tips:

To use betterlockscreen to lock when  lid closed with xfc4-power-manager.

------

```
xfconf-query -c xfce4-session -p /general/LockCommand -s "$(which betterlockscreen) -l" --create -t string
```

------

Tools:
------

[[Responder]] is a very useful tool for red team, physical access.
- Lets you poisin, sniff, etc for NTLM hashes.
- Github: https://github.com/lgandx/Responder

------
[[PCredz]] is a tool that lets you to sniff credentials on a number of protocols either from PCAP or live interface
- Github: https://github.com/lgandx/PCredz

------
[[UFW]] is a very simple and easy to use firewall. Very helpful to control access to certain ports.

------

[[Hakrevdns]] is a very simple and useful tool to get domains from ips using reverse dns lookup. Can also be piped easily into other tools like [[Httprobe]].

------

[[Httprobe]] is a simple golang tool that can check for http and https of a given domain. Can be used in conjuction with other tools like [[Hakrevdns]] through piping.

------
[[PCAPMonkey]] is a platform that uses zeek, suricata, and [[ELK]] to extract useful information from pcap files. Uses docker.

------

[[dirhunt]] is an interesting tool that allows getting paths without bruteforcing.

------

[[Gobuster]] is a golang tool for bruteforcing and is very fast with lots of options.

-------

Sniffers:
------

-  [[tcpdump]] by far the best packet sniffer from cli
-  [[p0f]] is an easy to use passive fingerprinting tool
- [[dsniff]] old but still reliable tool to sniff for plaintext

------

Data can be analyzed and viewed in [[Brute Shark]]