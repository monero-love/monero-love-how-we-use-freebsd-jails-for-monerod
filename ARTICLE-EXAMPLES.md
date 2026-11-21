# Published examples

Source: https://monero.love/guides/how-we-use-freebsd-jails-for-monerod/

Read the article for the ordering, prerequisites and version limits of these separate examples.

## Block 1

```text
install -d /usr/local/etc/pkg/keys /usr/local/etc/pkg/repos
fetch -o /usr/local/etc/pkg/keys/monero-love.pub \
    https://pkg.monero.love/monero-love.pub
```

## Block 2

```text
monero_love: {
  url: "https://pkg.monero.love/${ABI}/latest",
  enabled: yes,
  signature_type: "pubkey",
  pubkey: "/usr/local/etc/pkg/keys/monero-love.pub"
}
```

## Block 3

```text
pkg update
pkg install monerod-love
monerod-love --version
```

## Block 4

```text
sysrc monerod_love_enable=YES
service monerod_love start
```

## Block 5

```text
pkg update
pkg upgrade -n monerod-love
```

## Block 6

```text
ext_if = "ix0"
jail_ip = "10.170.100.10"
node_port = "18080"

set limit states 200000

nat on $ext_if inet from $jail_ip to any -> ($ext_if)
rdr on $ext_if inet proto tcp from any to ($ext_if) \
    port $node_port -> $jail_ip

pass in on $ext_if inet proto tcp from any to $jail_ip \
    port $node_port flags S/SA keep state

pass out on $ext_if inet from $jail_ip to any keep state
```

## Block 7

```text
pfctl -nf /etc/pf.conf
```

## Block 8

```text
kern.maxfiles=262144
kern.maxfilesperproc=131072
kern.ipc.soacceptqueue=4096
```

## Block 9

```text
sysctl kern.maxfiles=262144
sysctl kern.maxfilesperproc=131072
sysctl kern.ipc.soacceptqueue=4096
```

## Block 10

```text
procstat -l <PID>
procstat -f <PID>
```

## Block 11

```text
pfctl -si
pfctl -sm
sysctl kern.openfiles
netstat -Lan
netstat -m
```
