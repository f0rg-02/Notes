---
Name: dsniff
Platform: Linux
tags: Resources
---
dsniff is a tool for sniffing passwords from plaintext traffic. It comes as part of a suite of sniffing/snarfing tools that work like dsniff but extract other types of information (images, emails, URLs, etc.).

Very simple and useful. Can be used by pulling from pcap files or on a live interface.

Install:

```
sudo apt install dsniff
```

------

Usage:

```ruby
dsniff -i <interface>
```

Or:

```ruby
dsniff -i <interface> -p <pcapfile>
```

Seems useful for internal networks where plaintext traffic is probably more common

------