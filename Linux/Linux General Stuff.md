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

Sniffers:
------

-  [[tcpdump]] by far the best packet sniffer from cli 
-  [[p0f]] is an easy to use passive fingerprinting tool
- [[dsniff]] old but still reliable tool to sniff for plaintext

------

Data can be analyzed and viewed in [[Brute Shark]]