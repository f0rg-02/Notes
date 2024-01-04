# **Libvirt:**

Install libvirt first with package manager. For Debian/Ubuntu based distros, install `libvirt0` and `libvirt-dev`. For Arch Linux, `libvirt` is enough.

Then clear out existing plugins:

```ruby
vagrant plugin expunge -f
```

And install:

```ruby
vagrant plugin install vagrant-libvirt
```

------
# **General Usage:**

To download and initialize vagrant vm:

```ruby
vagrant init <box>

Example:

vagrant init ubuntu/trusty64
```

------

To bring VM up:

```ruby
vagrant up
```

------

To suspend:

```ruby
vagrant suspend
```

------

To ssh to vm:

```ruby
vagrant ssh
```