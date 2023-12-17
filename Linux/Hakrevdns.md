---
Name: Hakrevdns
Platform: Linux
tags:
  - Resources
  - infosec
---
GitHub: https://github.com/hakluke/hakrevdns

------

- Tool that lets you get domains from IPs by using reverse dns lookup

Install: `go install github.com/hakluke/ hakrevdns@latest`

------

Usage:

From README:

```Ruby
Usage

The most basic usage is to simply pipe a list of IP addresses into the tool, for example:

hakluke~$ prips 173.0.84.0/24 | hakrevdns
173.0.84.110	he.paypal.com.
173.0.84.109	twofasapi.paypal.com.
173.0.84.114	www-carrier.paypal.com.
173.0.84.77	twofasapi.paypal.com.
173.0.84.102	pointofsale.paypal.com.
173.0.84.104	slc-a-origin-pointofsale.paypal.com.
173.0.84.111	smsapi.paypal.com.
173.0.84.203	m.paypal.com.
173.0.84.105	prm.paypal.com.
173.0.84.113	mpltapi.paypal.com.
173.0.84.8	ipnpb.paypal.com.
173.0.84.2	active-www.paypal.com.
173.0.84.4	securepayments.paypal.com.
...

Piping to other programs like httprobe:

echo "173.0.84.110" | hakrevdns -d | httprobe
...
```

------