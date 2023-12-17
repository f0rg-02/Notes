---
Name: Get IPs from ASN
Platform: Linux
tags:
  - Resources
  - infosec
---
Required programs: prips, [[Hakrevdns]], [[Httprobe]]

Bash script:

```ruby
#!/usr/bin/env bash

# Fuck one liners you lazy buffoons.

# one-liner to convert ASN to ip addresses. Results will be appended to `ips.out`. sander@cedsys.nl | 1-7-2017
# Requires: sudo apt install prips httprobe

# If httprobe not found in apt: https://github.com/tomnomnom/httprobe
# Install httprobe: go install github.com/tomnomnom/httprobe@latest

# Also requires: https://github.com/hakluke/hakrevdns
# Install hakrevdns: go install github.com/hakluke/hakrevdns@latest

ASNFILE=""
OUTPUTFILE=""

usage() {  # Function: Print a help message.
  echo "Usage: $0 [ -f FILE OF ASNs to get IP addresses of ] [ -o OUTPUT FILE ] [ -h HELP ]" 1>&2
}

exit_abnormal() { # Function: Exit with error.
  usage
  echo "---------------"
  echo "Exiting!"
  exit 1
}

 while getopts "f:o:h" opt
 do
	 case ${opt} in
		f)
			echo "ASN file: ${OPTARG}"
			ASNFILE="${OPTARG}"
			;;
		o)
			echo "Final output file: ${OPTARG}"
			OUTPUTFILE="${OPTARG}"
			;;
		h)
			exit_abnormal
			;;
	esac
done

# Check if the arguments were inputted
if [[ -z "$ASNFILE" || -z "$OUTPUTFILE" ]]
then
	echo "[!] Not all required arugments were supplied"
	echo "---------------"
	exit_abnormal
	exit
fi

while IFS= read -r asn # Read file line by line
do
	for range in $(echo $(whois -h whois.radb.net -- "-i origin $asn" | grep -Eo "([0-9.]+){4}/[0-9]+") | sed ':a;N;$!ba;s/\n/ /g')
	do
		prips "$range" | hakrevdns -d | httprobe >> "$OUTPUTFILE"
	done
done < "$ASNFILE"
```

Usage: `./domains_from_asn.sh -f <file of asn to get ips from> -o <output file to save results>` ^82ecb6

-------

Test script:

```ruby

#!/bin/bash

# one-liner to convert ASN to ip addresses. Results will be appended to `ips.out`. sander@cedsys.nl | 1-7-2017
# requires: apt-get install prips

for asn in AS51468 AS37061 AS198810 AS39513;
    do $(for range in $(echo $(whois -h whois.radb.net -- "-i origin $asn" | grep -Eo "([0-9.]+){4}/[0-9]+") | sed ':a;N;$!ba;s/\n/ /g');
        do prips $range > ranges.out
    done);
done

while IFS= read -r line
do
    echo $line | hakrevdns -d | httprobe
done < ranges.out

```

- Original script that I used to test this out