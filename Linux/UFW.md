---
Name: UFW
Platform: Linux
tags: Resources
---
- UFW stands for **Uncomplicated Firewall** and is a free, simple, firewall program for Linux.
- Very simple to install: `sudo apt install ufw`
- To add rules: `sudo ufw allow` followed by the port or service.

Example:

```ruby
sudo ufw allow OpenSSH # Add OpenSSH service
sudo ufw allow ssh # Add the ssh service whatever
sudo ufw allow 22 # Add port for ssh
sudo ufw allow 3389 # Add the port for rdp
sudo ufw allow 9090 # Add the web port for cockpit
sudo ufw allow 10000 # Add the web port for wedmin
sudo ufw show added # Lists all the rules added
sudo ufw enable # Enable firewall
```

**NOTE: For every new port opened a firewall rule needs to be added**

Show all the rules added:

```ruby
sudo ufw show added
```

To allow any from an ip:

```ruby
sudo ufw allow from <ip> to any
```

To deny any from an ip:

```ruby
sudo ufw deny from <ip> to any
```

To delete rule:

```ruby
sudo ufw delete allow <port> # Allow rules
sudo ufw delete deny <port> # Deny rules
sudo ufw delete <number_of_rules>
```

To show status:

```ruby
sudo ufw status # Regular
sudo ufw status numbered # Numbered
```

