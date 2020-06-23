# Alpine VPN Framework (AVF)

This tool will (hopefully) make it trivial to setup an Alpine Linux
box as a VPN box. It only supports OpenVPN (with optional obfsproxy)
and Wireguard at this point in time.

## Setup

All below steps assume you are `root`.

1. Install Alpine
    - Ensure you are running `edge` and are fully up-to-date

```
$ cat /etc/apk/repositories
https://<mirror.hostname>/alpinelinux/edge/main
https://<mirror.hostname>/alpinelinux/edge/community
https://<mirror.hostname>/alpinelinux/edge/testing
$ apk update
$ apk upgrade -a -U
```

2. Install bash and git

```
$ apk add bash git
```

3. Clone AVF

```
$ git clone https://gitlab.com/mjwhitta/avf.git
$ cd ./avf
```

4. Run `prep` to install dependencies

```
$ ./prep
```

5. Install `avf` and read usage to follow the remaining setup

```
$ ./installer
$ avf -h
```

**Note:** Ensure that `~/.local/bin` is in your `$PATH`.
