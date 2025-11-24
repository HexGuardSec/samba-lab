# Samba Network Lab

## Project Overview

This project is a **Samba network lab** that demonstrates a multi-user file sharing setup in Linux.
It consists of one server (`srv-linux`) and two virtual machines:

* **Emilie** – Accountant (can access `commun` and `compta`)
* **Clement** – Developer (can access `commun` and `dev`)

The goal is to simulate a real-world environment where users access shared folders based on group permissions. This lab is ideal for learning Samba configuration, Linux user/group management, file permissions, and network connectivity.

### Shared Folders

* **commun** – accessible by all users or members of the `hexcompany` group
* **dev** – accessible only by the developer group (`devs`)
* **compta** – accessible only by the accountant group (`compta`)

---

## Repository Structure

The repository is organized as follows:

* `README.md` – this file with project overview and instructions
* `LICENSE` – MIT License
* `docs/` – documentation for the lab

  * `architecture.md` – network diagram and group permissions
  * `setup-guide.md` – step-by-step setup instructions

* `configs/` – configuration files

  * `smb.conf` – Samba configuration with comments
  * `passwd.txt` – lab users
  * `enp0s8-config.yaml` – Netplan configuration

* `screenshots/` – images showing lab functionality

  * `ping_srv_emilie.png` – ping test Emilie → server
  * `ping_srv_clement.png` – ping test Clement → server
  * `dev_access.png` – access to `dev` folder
  * `compta_access.png` – access to `compta` folder
  * `write_test_commun(compta).png` - the group compta can write in `commun` folder
  * `write_test_commun(dev).png` - the group dev can write in `commun` folder
  * `write_test_compta.png` - the group compta can write in `compta` folder
  * `write_test_dev.png` - the group dev can write in `dev` folder

---

## Network Architecture

The lab consists of one server and two VMs connected in the same network:

* **Server (`srv-linux`)** – hosts the Samba shares
* **VM Emilie (Accountant)** – accesses `commun` and `compta`
* **VM Clement (Developer)** – accesses `commun` and `dev`

### Samba Shares & Permissions

| Share Folder | Accessible By                   | Description           |
| ------------ | ------------------------------- | --------------------- |
| commun       | Company employee (`hexcompany`) | General shared folder |
| dev          | Developers (`devs`)             | Development folder    |
| compta       | Accountants (`compta`)          | Accounting folder     |

---

## Setup Instructions

1. **Clone the repository**
   `git clone https://github.com/<your-username>/samba-lab.git`
   `cd samba-lab`

2. **Create groups and users**

```bash
sudo groupadd devs
sudo groupadd compta
sudo useradd emilie -G compta
sudo useradd clement -G devs
sudo smbpasswd -a emilie
sudo smbpasswd -a clement
```

3. **Create shared folders**

```bash
sudo mkdir -p /srv/samba/commun
sudo mkdir -p /srv/samba/dev
sudo mkdir -p /srv/samba/compta

sudo chown :devs /srv/samba/dev
sudo chown :compta /srv/samba/compta
sudo chmod 770 /srv/samba/dev
sudo chmod 770 /srv/samba/compta
sudo chmod 777 /srv/samba/commun
```

4. **Apply Samba configuration**

* Copy `configs/smb.conf` to `/etc/samba/smb.conf`
* Restart Samba: `sudo systemctl restart smbd`

5. **Test access from each VM**

* Emilie → `commun` & `compta`
* Clement → `commun` & `dev`
* Use `ping` and `smbclient` or file explorer to verify access

---

## Screenshots

* **Network connectivity**

  * `ping_srv_emilie.png`
  * `ping_srv_clement.png`

* **Samba shares**

  * `compta-access.png`
  * `dev-access.png`

---

## License

This project is licensed under the **MIT License**.
