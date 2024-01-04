---
Name: Add user to vbox group
Platform: Linux
tags:
  - Resources
  - general
---

Add user to vbox group:

```ruby
sudo usermod -a -G vboxusers $USER
```

------

Log out and log back in.

To check run:

```ruby
groups $USER
```

------
Links:
- SO Post: https://askubuntu.com/questions/377778/how-to-add-users-to-vboxusers-to-enable-usb-usage/377781#377781
- Archived SO Post: https://askubuntu.com/questions/377778/how-to-add-users-to-vboxusers-to-enable-usb-usage/377781#377781