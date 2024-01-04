---
Name: Fix Unable to Ping Domains
Platform: Linux
tags:
  - Resources
  - general
---


Sometimes can ping dns and ips, but not domain names. Annoying especially on my Debian server.

The solution I found to work is to change this line in /etc/nsswitch.conf:

From this:

```
hosts:          files mdns4_minimal [NOTFOUND=return] dns myhostname
```

- Or whatever is on the hosts line

To this:

```
hosts:          files dns
```

------

Link to solution:
- https://unix.stackexchange.com/a/394657
- Archived: https://web.archive.org/web/2/https://unix.stackexchange.com/questions/39071/debian-problem-with-dns/394657#394657