## VM1

Netplan configuration at `/etc/netplan/60-my-init.yaml`

```
network:
  version: 2
  ethernets:
    enp0s8:
      # dhcp4: true
      addresses:
        - 192.168.56.10/24
        - 192.168.56.11/24
```

Apply netplan:

```
sudo netplan apply
```

Add this to SSHD config at `/etc/ssh/sshd_config`

```
ListenAddress 192.168.56.10
```

## VM2

Config IP:

```
sudo nmcli connection add type ethernet con-name enp0s8 ifname enp0s8 autoconnect yes ipv4.method manual ipv4.addresses 192.168.56.9/24
```
