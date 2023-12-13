---
Name: Nmap
Platform: Linux
tags: Resources
---

The <mark style="background: #FF5582A6;">**GOAT**</mark> of port scanning.

Install:

```bash
sudo apt install nmap
```

Some of my favorite nmap scans:

```bash
sudo nmap -Pn -v --open -p <port> ip_range
```

Example: `sudo nmap -Pn -v --open -p22 172.16.42.1/24` <- to check if ssh port is open on the wifi pineapple local subnet.

```bash
sudo nmap -sS -Pn -v --open ip_range
```

Syn scan.

------

```bash
sudo nmap -sV -Pn -v --open ip_range
```

Service scan. Can add `-A` to do fingerprinting and OS detection.

------

```bash
sudo nmap -sF -Pn -v --open ip_range
```

Fin scan. Supposed to be stealthier.

------

```bash
sudo nmap -sT -Pn -n -v --open ip_range
```

TCP Scan with no ping and prevent dns lookup or whatever.

------