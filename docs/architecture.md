# Network Architecture

This lab consists of one Linux server and two virtual machines:

* **Server**: `srv-linux` – hosts Samba shares.
* **VM 1**: Emilie (Accountant) – can access `commun` and `compta` shares.
* **VM 2**: Clement (Developer) – can access `commun` and `dev` shares.

**Connectivity**

* All machines can communicate with each other via ping.
* Network traffic is internal to the lab environment.

**Samba Shares & Permissions**

| Share Folder | Accessible By | Description                  |
| ------------ | ------------- | ---------------------------- |
| `commun`     | All users     | General file sharing folder  |
| `dev`        | Developers    | Folder for development files |
| `compta`     | Accountants   | Folder for accounting files  |

**Diagram**

```
        +----------------+
        |   srv-linux    |
        | Samba Server   |
        +-------+--------+
                |
       -------------------
       |                 |
+-------------+    +-------------+
| Emilie VM   |    | Clement VM  |
| Accountant  |    | Developer   |
+-------------+    +-------------+
```

This diagram shows which VMs can access which folders based on their user group.

---