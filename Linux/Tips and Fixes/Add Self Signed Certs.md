---
Name: Add self signed certs
Platform: Linux
tags: Resources
---
**NOTE: FOR TESTING!!! DO NOT USE SELF SIGNED IN PRODUCTION!!!**

On debian install `ca-certificates` but most likely already installed:

```ruby
sudo apt-get install ca-certificates
```

Copy the certificate with `.crt` extension:

```ruby
cp cacert.crt /usr/share/ca-certificates
```

And then reconfigure `ca-certificates`:

```ruby
sudo dpkg-reconfigure ca-certificates
```

When prompted, select and press **ENTER** to activate the cert.

------

Link to [original](https://unix.stackexchange.com/a/90607) and link to [archive](https://web.archive.org/web/20230729053542/https://unix.stackexchange.com/questions/90450/adding-a-self-signed-certificate-to-the-trusted-list/90607)

------
