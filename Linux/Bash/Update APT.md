---
Name: Bash Update APT
Platform: Debian distros
tags:
  - Resources
  - general
---
Bash script to update system using APT:

```ruby
#!/usr/bin/env bash

echo "[*] Starting system update"

sudo apt update && sudo apt --assume-yes upgrade
sudo apt --assume-yes dist-upgrade
sudo apt --assume-yes full-upgrade
sudo apt --assume-yes autoremove
sudo apt --assume-yes autoclean

echo "[*] Done"
```