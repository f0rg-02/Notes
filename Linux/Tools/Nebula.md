GitHub: https://github.com/slackhq/nebula

------
- VPN mesh network by Slack
- Relatively simple and has its own firewall that can be used in conjunction with [[UFW]]
	- UFW add ip of TUN device that nebula is using to allow from any port

------
Docs: https://nebula.defined.net/docs/
Docs quickstart: https://nebula.defined.net/docs/guides/quick-start/

------

Start:
------

Create CA: `nebula-cert ca -name "Whatever Org, Inc"`

This creates the root certs in current directory. Change permissions: `chmod 600 ca.key`

------
To create new nodes: 

```
sudo nebula-cert sign -name "lighthouse" -ip "192.168.100.1/24"
sudo nebula-cert sign -name "laptop" -ip "192.168.100.5/24"
sudo nebula-cert sign -name "server" -ip "192.168.100.9/24"
```

Each set of certs should be transferred to their respective devices via some method.

-------

```
Client config I used:

```yaml
pki:
  ca: /etc/nebula/ca.crt
  cert: /etc/nebula/laptop.crt
  key: /etc/nebula/laptop.key

static_host_map:
  "10.10.10.1": ["192.168.1.170:4242", "192.168.8.174:4242"]

lighthouse:
  hosts:
    - "10.10.10.1"

punchy:
  punch: true

firewall:

  outbound:
    - port: any
      proto: any
      host: any

  inbound:
    - port: any
      proto: any
      host: any 

```


Client server I used:

```yaml
pki:
  ca: /etc/nebula/ca.crt
  cert: /etc/nebula/lighthouse.crt
  key: /etc/nebula/lighthouse.key

lighthouse:
  am_lighthouse: true

punchy:
  punch: true

firewall:

  outbound:
    - port: any
      proto: any
      host: any

  inbound:
    - port: any
      proto: any
      host: any 

```

To start: `sudo nebula -config config.yml`

------

Service:
------

There is a service file, but might have to add it manually. 

Service config:

```
[Unit]
Description=nebula
Wants=basic.target network-online.target
After=basic.target network.target network-online.target

[Service]
SyslogIdentifier=nebula
ExecReload=/bin/kill -HUP $MAINPID
ExecStart=/usr/bin/nebula -config /etc/nebula/config.yml
Restart=always

[Install]
WantedBy=multi-user.target

```

Add to the systemd system folder and run:

```
sudo chmod +x <path_to_system_file> # probably not needed
sudo systemctl daemon-reload
sudo systemctl start nebula.service
sudo systemctl enable nebula.service
```