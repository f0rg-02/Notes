---
Name: Zerotier
Platform: Linux
tags: Resources
---
A tool that allows to setup peer-to-peer networks. Very useful and runs on multiple different platforms including windows, linux, openwrt, raspberry pi, etc.

To install on Linux:

```bash
curl -s https://install.zerotier.com | sudo bash
```

Check before to see if already in repository.

Enable the service so it will start on boot. Also make sure <mark style="background: #FF5582A6;">ufw is disabled</mark> or else zerotier can't connect to the "moons" or whatever zerotier calls their relay servers.

```bash
sudo systemctl enable zerotier-one
```

See status of zerotier. Helpful with troubleshooting.

```bash
sudo zerotier-cli status
```

------

You need to go to [zerotier website](https://www.zerotier.com/) and either sign in or sign up. Create a new network and use the ID to join the device:

```bash
sudo zerotier-cli join [Network ID]
```

You will need to authenticate the device in the dashboard of your account. This is a way to help prevent random devices from joining. <mark style="background: #FF5582A6;">**DO NOT DISABLE THIS!!!**</mark> There is an option to let people disable it, but don't.

You can either verify with:

```bash
sudo zerotier-cli listnetworks 
```

Or just check `ip a` to see if the interface has an IP.

A nice guide: https://raspiserver.com/how-to-install-zerotier-on-raspberry-pi/ ^adf089