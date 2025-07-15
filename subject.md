# Born2beRoot

## 📘 Project Overview

**Born2beRoot** is a System Administration project from the 42 curriculum.  
Its goal is to introduce students to virtualization and server setup under strict security and configuration constraints.

> **Disclaimer:**  
> This document is an unofficial summary written for educational and documentation purposes.  
> It is not affiliated with or endorsed by 42 or its partners.  
> All 42 students are responsible for adhering to the academic integrity policy.  
> You may **not** publish or share any part of the official subject PDF, evaluation scripts, or Moulinette content.

---

## Contents

- [Goals](#goals)
- [General Guidelines](#general-guidelines)
- [Mandatory Part](#mandatory-part)
- [Bonus Part](#bonus-part)
- [Submission Guidelines](#submission-guidelines)

---

## Goals

- Set up a secure Linux-based virtual server.
- Learn about encryption, user rights, firewall configuration, and monitoring scripts.
- Use either **Debian (recommended)** or **Rocky Linux (advanced)**.

---

## General Guidelines

- You **must** use **VirtualBox** or **UTM** (if VirtualBox is not possible).
- Submit only a `signature.txt` file containing the SHA1 signature of your virtual disk.
- The project requires a CLI-only setup — graphical environments like X.org are strictly **forbidden**.

---

## Mandatory Part

### 🧱 Operating System Setup

- Use **latest stable Debian** or **Rocky Linux**.
- Must have at least **2 encrypted LVM partitions**.
- Enable **SELinux** (Rocky) or **AppArmor** (Debian) on startup.

### 🔐 SSH

- SSH must run on **port 4242**.
- **Root login via SSH must be disabled**.
- SSH usage will be tested during the defense.

### 🔥 Firewall

- **Debian**: use **UFW**.
- **Rocky**: use **firewalld**.
- Only port **4242** should be open.

### 🖥️ Hostname

- Must be your **login** + `42` (e.g., `wil42`).
- You’ll be asked to change the hostname during evaluation.

### 👥 User Management

- Root + a user with your **login** must exist.
- Your user must belong to `sudo` and `user42` groups.

### 🔒 Password Policy

- Expire every **30 days**.
- Min change delay: **2 days**.
- Warning: **7 days** before expiry.
- Minimum **10 characters**, with:
  - 1 uppercase
  - 1 lowercase
  - 1 number
  - Max 3 identical consecutive characters
  - No username in password
  - New password must differ from previous (except for root)
- Apply policy to **all accounts** on VM.

### 🔧 Sudo Configuration

- Max **3 authentication attempts**
- Custom error message on wrong password
- **Log all commands** (inputs & outputs) to `/var/log/sudo/`
- **TTY mode enabled**
- **Path restriction**:
  ```
  /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
  ```

### 🛠️ Monitoring Script

Create a Bash script named `monitoring.sh` that:

- Displays a system report **every 10 minutes** via `wall`.
- No errors must appear.
- Must display:
  - Architecture & kernel
  - Physical & virtual CPUs
  - RAM usage
  - Disk usage
  - CPU load
  - Last reboot date
  - LVM usage
  - Active TCP connections
  - Logged-in users
  - IPv4 + MAC address
  - Number of `sudo` commands run

> You will be asked to explain and **stop the script without modifying it**. Look into `cron`.

---

## Bonus Part

- Proper LVM partition layout
- Functional **WordPress** setup with:
  - `lighttpd`
  - `MariaDB`
  - `PHP`
- Additional service (e.g., **FTP**, **DNS**, **Redis**, **Mail**, etc.)  
  ⚠️ **NGINX / Apache2 are forbidden**
- Adjust firewall rules accordingly

> ⚠️ **Bonus will only be evaluated if the mandatory part is PERFECT.**

---

## Submission Guidelines

- Only submit `signature.txt` at the repo root.
- To get your disk signature:

### Virtual Disk Paths

| OS        | Path |
|-----------|------|
| Windows   | `%HOMEDRIVE%%HOMEPATH%\VirtualBox VMs\` |
| Linux     | `~/VirtualBox VMs/` |
| macOS     | `~/VirtualBox VMs/` |
| Mac M1 + UTM | `~/Library/Containers/com.utmapp.UTM/Data/Documents/` |

### Commands to Get SHA1 Signature

```bash
# Windows
certUtil -hashfile rocky_serv.vdi sha1

# Linux
sha1sum rocky_serv.vdi

# macOS
shasum rocky_serv.vdi

# Mac M1 (UTM)
shasum rocky.utm/Images/disk-0.qcow2
```

Example output:
```
6e657c4619944be17df3c31faa030c25e43e40af
```

⚠️ **Do NOT submit the VM itself**  
⚠️ **Do NOT alter the virtual disk after signature**  
Use "save state" or duplicate VM to preserve signature.

---

