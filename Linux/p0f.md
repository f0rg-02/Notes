---
Name: p0f
Platform: Linux
tags: Resources
---
Passive OS Fingerprint and Network Analysis. Useful over nmap because it doesn't send active probes like Nmap does.

Install:

```
sudo apt install p0f
```

------

Basic Usage:

```ruby
p0f -i eth0 -p -o /tmp/p0f.log
```

------

Passive is useful to stay less noisy.