# Samba Setup Guide

## Requirements

* Linux server (Ubuntu/Debian recommended)
* Samba installed (`sudo apt install samba`)
* Two VMs configured on the same network

## Step 1: Network Setup

1. Ensure all machines can ping each other:

```bash
ping <server-ip>
ping <emilie-ip>
ping <clement-ip>
```

## Step 2: Create Groups

```bash
sudo groupadd dev
sudo groupadd compta
```

## Step 3: Add Users

```bash
sudo useradd emilie -G compta
sudo useradd clement -G dev
```

## Step 4: Configure Samba Shares

* Create folders:

```bash
sudo mkdir -p /srv/samba/commun
sudo mkdir -p /srv/samba/dev
sudo mkdir -p /srv/samba/compta
```

* Set permissions:

```bash
sudo chown :dev /srv/samba/dev
sudo chown :compta /srv/samba/compta
sudo chmod 770 /srv/samba/dev
sudo chmod 770 /srv/samba/compta
sudo chmod 777 /srv/samba/commun
```

* Configure `/etc/samba/smb.conf` (Included in `configs/` folder).

## Step 5: Test Samba

* From each VM, try accessing the shares:

```bash
smbclient //srv-linux/commun -U emilie
smbclient //srv-linux/dev -U clement
```

* Only allowed users should access the restricted shares.

## Step 6: Troubleshooting

* Check Samba status:

```bash
sudo systemctl status smbd
```