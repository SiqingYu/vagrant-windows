# My Vagrant on Windows Tips

## Configuration

### Environment

* Hypervisor (Vagrant Provider): Virtualbox
* Vagrant on Windows

### Networking

The default networking mode of Vagrant is host-only network.

Network services (e.g, SSH's 22, HTTP's 80) can be accessed from WSL directly.

No need for port forwarding.

### SSH config

The command `vagrant ssh-config` shows misleading messages.

It shows the port as 2200 by default, but it means the 22 guest port is forwarded to the 2200 host port.

It also shows that password authentication is not allowed, but in fact I tried login in from WSL with password and it works.

Instead, `/etc/ssh/sshd_config` in the Vagrant machine shows that the default config is port 22 and allows password authentication.

The correct guest SSH port can be seen in the `vagrant up` messages.

```
==> default: Forwarding ports...
    default: 22 (guest) => 2200 (host) (adapter 1)
```

## Usages

### Login from WSL

The private key is not needed.

```
ssh 192.168.33.10 -l vagrant
```

The password is also `vagrant`.

## Other Options?

### Why not Hyper-V?

Hyper-V's networking is not configurable by Vagrant, and its default network switch does not allow connection from WSL in the WSL Hyper-V switch.

Reference:
https://www.vagrantup.com/docs/providers/hyperv/limitations

### Why not Vagrant inside WSL?

Vagrant in WSL still uses the hypervisor on the Windows host, so there is no practical advantage.

One nuisance is that Vagrant in WSL can only use Vagrantfile on the Windows host file system.

I haven't tried nested virtualization inside WSL yet, maybe I should give KVM a shot someday.
