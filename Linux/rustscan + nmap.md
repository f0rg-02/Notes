---
Name: rustscan_map
Platform: Linux
tags:
  - Resources
  - Shells
---

Script to run rustscan to quickly get open ports before running through nmap for more detailed scan.

Example usage: `sudo ./rustscan_map.sh -f test_hostfile.txt -n test_nmap.xml -o test_results.txt -p21,22,80,443,8080,2121`

#todo
- [ ] Figure out how to inserts the results into a database

------

```bash
#!/usr/bin/env bash

HOSTFILE=""
PORTS=""
OUTPUTFILE=""
NMAPFILE=""

UUID=$(uuidgen)

usage() {  # Function: Print a help message.
  echo "Usage: $0 [ -f FILE OF IPS TO SCAN  ] [ -n NMAP OUTPUT FILE ] [ -o OUTPUT FILE ] [ -p PORTS ] [ -h HELP ]" 1>&2
}

exit_abnormal() { # Function: Exit with error.
  usage
  echo "---------------"
  echo "Exiting!"
  exit 1
}

 while getopts "f:n:p:o:h" opt
 do
	 case ${opt} in
		f)
			echo "IP file: ${OPTARG}"
			HOSTFILE="${OPTARG}"
			;;
		n)
			echo "Nmap output file: ${OPTARG}"
			NMAPFILE="${OPTARG}"
			;;
		p)
			echo "Ports to scan: ${OPTARG}"
			PORTS="${OPTARG}"
			;;
		o)
			echo "Rustscan output file: ${OPTARG}"
			OUTPUTFILE="${OPTARG}"
			;;
		h)
			exit_abnormal
			;;
	esac
done

if [[ -z "$HOSTFILE" || -z "$PORTS" || -z "$OUTPUTFILE" || -z "$NMAPFILE" ]]
then
	echo "[!] Not all required arugments were supplied"
	echo "---------------"
	exit_abnormal
	exit
fi

# Create directory to store results in
mkdir -p nmap_scans/"$UUID"

sudo rustscan -a "$HOSTFILE" -p "$PORTS" --ulimit 5000 --greppable > "$OUTPUTFILE"

sed -i 's/->/-/g' "$OUTPUTFILE"

declare -a port_array

while IFS= read -r line
do
    NMAP_UUID=$(uuidgen)
    cut_ip=$(echo "$line" | cut -d "-" -f1)
    cut_port=$(echo "$line" | cut -d "[" -f2 | cut -d "]" -f1)     
    port_array=${cut_port[@]}
    echo "Ip is: $cut_ip"
    echo "Ports are: ${port_array[@]}"
    echo "---------------"
    sudo nmap -T4 -Pn -vv -A --open -p $cut_port -oX nmap_scans/"$UUID"/"$NMAP_UUID"_"$NMAPFILE" $cut_ip
    echo "---------------"
done < "$OUTPUTFILE"
echo "Done!"

```