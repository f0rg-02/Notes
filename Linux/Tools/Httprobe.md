---
Name: Httprobe
Platform: Linux
tags:
  - Resources
  - infosec
---
GitHub: https://github.com/tomnomnom/httprobe

------

- Allows to pipe domains and check for http and https
	- Outputs to stdout which can then be redirected toward a file

Install: `go install github.com/tomnomnom/httprobe@latest`

------

Usage:

```Ruby
cat domain_list.txt | httprobe
cat domain_list.txt | httprobe > output_file.txt

With hakrevdns:

echo "173.0.84.110" | hakrevdns -d | httprobe
```

------