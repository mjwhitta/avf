# Alpine VPN Framework (AVF)

[![Yum](https://img.shields.io/badge/-Buy%20me%20a%20cookie-blue?labelColor=grey&logo=cookiecutter&style=for-the-badge)](https://www.buymeacoffee.com/mjwhitta)

This tool will (hopefully) make it trivial to setup an Alpine Linux
box as a VPN box. It only supports OpenVPN (with optional obfsproxy)
and Wireguard at this point in time.

## Setup

All below steps assume you are `root` on a clean install of Alpine (1
CPU, 128MB RAM, 8GB disk).

1. Install bash and git

```
$ apk add --update bash git
$ exec bash
```

2. Clone AVF

```
$ git clone https://github.com/mjwhitta/avf.git
$ cd ./avf
```

3. Run `prep` to install dependencies (optionally obfsproxy support)

```
$ ./prep [--obfs]
```

4. Reboot when requested, then read `avf` usage to setup VPNs

```
$ avf -h
```

**Note:** It is important to note that OpenVPN uses the
`255.255.255.0` syntax for netmasks, but Wireguard uses `/24`.

## Optional configuration

You can modify `/etc/dnsmasq.d/default.conf` to change upstream DNS
servers (default: 8.8.8.8).

You can modify `/etc/local.d/z_user.start` and
`/etc/local.d/z_user.stop` to start/stop custom services with the
`local` service. A common use-case would be connecting to an upstream
VPN on boot.

If you want to use this as a VPN gateway (rather than VPN access to
your home), you will need to add something like the following to
`/etc/network/interfaces`:

```
auto eth0
iface eth0 inet dhcp
    post-up ip r a 192.168.0.0/16 via <gateway> dev eth0
```

Then read the comments in `avf fw` and adjust your firewall as needed.
