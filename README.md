Parfait ! Voici une version **pro, GitHub-friendly et agréable à lire**, prête à copier-coller dans ton README :
# 🖥️ Samba Lab Project

## 📖 Overview

This project simulates a **small company network** using virtual machines (VMs).
The main goal is to practice **file sharing management** with **Samba** on Linux servers.

## 🌐 Network Setup

* **Server VM**: Ubuntu Server hosting the shared folders.
* **Client VMs**: Kali Linux machines (**Alice**, **Bob**, **Charlie**) acting as company workstations.
* All VMs communicate over an **internal network** with static IPs.

## 🗂️ Samba Configuration

* **Shared folder**: `/srv/partage` on the server.
* **Bob**: ✅ read/write access
* **Alice**: 🔒 read-only access
* **Charlie**: ✅ read/write access
* Samba service is configured to allow **controlled access** for each user based on their permissions.

**Key settings in `smb.conf`:**

```ini
[partage]
   path = /srv/partage
   browsable = yes
   read only = no
   guest ok = no
   create mask = 0777
   directory mask = 0777
```

## ⚡ Features Demonstrated

* 👥 Creation of multiple users and groups.
* 🔐 Management of file permissions and ownership.
* 🖇️ Mounting Samba shares from client machines.
* 📂 Testing user access rights (read/write).
* 🌐 Network connectivity between server and clients.


## 📸 Screenshots

Include screenshots to demonstrate:

1. VM consoles showing **usernames and IP addresses**.
2. **Server folder structure** and permissions.
3. **Samba configuration** file (`smb.conf`).
4. Successful mounting and accessing of shares from **each client**.

