# My Vagrant on Windows config template

## Environment

* Hypervisor (Vagrant Provider): Virtualbox
* Vagrant on Windows

## Networking

The default networking mode of Vagrant is host-only network.

Network services (e.g, SSH's 22, HTTP's 80) can be accessed from WSL directly.

No need for port forwarding.

## SSH config

The command `vagrant ssh-config` shows misleading messages.

It shows the port as 2200 by default, but it means the 22 guest port is forwarded to the 2200 host port.

It also shows that password authentication is not allowed, but in fact I tried logging in from WSL with password and it works.

Instead, `/etc/ssh/sshd_config` in the Vagrant machine shows that the default config is port 22 and allows password authentication.

The correct guest SSH port can be seen in the `vagrant up` messages.

```
==> default: Forwarding ports...
    default: 22 (guest) => 2200 (host) (adapter 1)
```

## Login from WSL

The private key is not needed.

```
ssh 192.168.33.10 -l vagrant
```

The password is also `vagrant`.
