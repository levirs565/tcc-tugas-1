## VM1

After installing VM, add Host-only adapter.

Netplan configuration at `/etc/netplan/60-my-init.yaml`

```
network:
  version: 2
  ethernets:
    enp0s8:
      addresses:
        - 192.168.56.10/24
        - 192.168.56.11/24
```

Apply netplan:

```
sudo netplan apply
```

Now you can connect to VM with SSH.

Add this to SSHD config at `/etc/ssh/sshd_config`

```
ListenAddress 192.168.56.10
```

Apply SSHD config:

```
sudo systemctl daemon-reload
sudo systemctl restart ssh.socket
```

Install Git:

```
sudo dnf install git
```

## VM2

After installing VM, add Host-only adapter.

Config IP:

```
sudo nmcli connection add type ethernet con-name enp0s8 ifname enp0s8 autoconnect yes ipv4.method manual ipv4.addresses 192.168.56.9/24
```

Install Git:

```
sudo apt install git
```

Now you can connect to VM with SSH.

Create directory for NFS:

```
mkdir vm2/nfs_share/gitea_repos
mkdir vm2/nfs_share/vikunja_files
```

## Starting Service

Start service using Docker Compose.
