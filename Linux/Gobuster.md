---
Name: Gobuster
Platform: Linux
tags:
  - Resources
  - infosec
---
GitHub: https://github.com/OJ/gobuster

Fast directory bruteforcer.

Install: `go install github.com/OJ/gobuster/v3@latest`

Command I found to be good enough for what I need: `gobuster dir -u <url> -w <wordlist> --quiet --no-color -e --hide-length -b "" -s 200`

Need to write a bash script that watches a directory for a new text file of domains to loop through and run through gobuster. Can probably combine using other sources like https://crt.sh/ via [[Lookup crt.sh]] script and [[Hakrevdns]] in combination with [[Httprobe]]

------