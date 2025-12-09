

## ✅ **I. Core Concepts & Tools (Foundational Knowledge)**

### 🔹 Virtualization & Environment Setup
- [ ] Learn **VirtualBox** (or **UTM** for Apple Silicon); compare both
  - VM creation, disk formats (`.vdi`, `.qcow2`)
  - How to locate VM files and compute SHA1 signature
  - Why snapshots are forbidden (and how to avoid them)
- [ ] Understand VM security: no GUI/X.org/Wayland → headless server setup

### 🔹 OS Choice & Comparison
- [ ] Research & compare **Debian (stable)** vs **Rocky Linux**
  - Pros/cons: package management (`apt` vs `dnf`), stability, SELinux/AppArmor defaults
  - Decide which to use (Debian recommended for beginners)
- [ ] Understand:
  - `apt` vs `aptitude`
  - Debian Stable vs Testing/Unstable — why only *stable* is allowed

---

## ✅ **II. Mandatory Part: System Setup & Hardening**

### 🔹 Disk & Storage
- [ ] Learn **LVM (Logical Volume Management)**
  - Create ≥2 **encrypted partitions** (e.g., with `cryptsetup + LUKS`)
  - Understand physical vs logical volumes, volume groups
- [ ] Plan partitioning scheme (e.g., `/`, `/home`, `/var`, swap)
  - Estimate appropriate disk sizes (minimal, but functional)
- [ ] Verify LVM activation at runtime (`lsblk`, `lvs`, `vgs`, `pvs`)

### 🔹 Security Hardening
- [ ] **Strong Password Policy**
  - Configure `/etc/login.defs`, `/etc/pam.d/common-password` (Debian) or `/etc/security/pwquality.conf` (Rocky)
  - Enforce:
    - 30-day expiry, 2-day min reuse, 7-day warn
    - ≥10 chars, upper/lower/digit, no >3 repeated chars, no username
    - Change all passwords post-configuration (incl. root)
- [ ] **Firewall Setup**
  - Learn **UFW** (Debian) vs **firewalld** (Rocky)
  - Allow only port `4242` (SSH); deny all else
  - Ensure firewall auto-starts at boot
- [ ] **SELinux (Rocky)** or **AppArmor (Debian)**
  - Ensure it’s *enforcing* at boot
  - Understand core concepts: MAC vs DAC, profiles/policies
  - Adapt config if needed (esp. for SSH/sudo/monitoring)

### 🔹 User & Access Management
- [ ] Create user: `<login>` (e.g., `wil`)
  - Add to groups: `sudo` and new custom group `user42`
- [ ] Disable **root SSH login**
  - Configure `/etc/ssh/sshd_config`: `PermitRootLogin no`, `Port 4242`
  - Restart SSH & test with new user
- [ ] **Sudo Hardening**
  - `/etc/sudoers` (`visudo`):
    - Limit retries to 3
    - Custom `badpass_message`
    - Enable `tty_tickets`
    - Log all I/O to `/var/log/sudo/`
    - Restrict `secure_path` to whitelisted dirs
  - Create `/var/log/sudo/` and test logging

### 🔹 System Identification & Config
- [ ] Set hostname to `<login>42` (e.g., `wil42`)
  - Use `hostnamectl` or edit `/etc/hostname`
  - Ensure persistent after reboot
- [ ] Set correct timezone (if required)

---

## ✅ **III. Monitoring Script (`monitoring.sh`)**
- [ ] Learn **Bash scripting best practices**
- [ ] Commands to gather:
  - Architecture & kernel: `uname -a`
  - Physical/virtual CPUs: `lscpu`, `nproc`, `/proc/cpuinfo`
  - RAM: `free -m`, `vmstat`, `/proc/meminfo`
  - Disk: `df -BG`, `lsblk`
  - CPU load: `top -bn1`, `awk '/cpu /{...}' /proc/stat`
  - Last boot: `who -b`, `systemctl list-boots`
  - LVM active: `lsblk -f`, `lvs`
  - TCP connections: `ss -t`, `netstat -tn`
  - Logged-in users: `who`, `w`, `users`
  - IPv4 & MAC: `ip a`, `hostname -I`, parse `ip link`
  - Sudo commands count: parse `/var/log/sudo/*` or use `journalctl`
- [ ] Use `wall` to broadcast to all TTYs
- [ ] Schedule with **cron**: `@reboot` + every 10 min (`*/10 * * * *`)
- [ ] Ensure no errors (redirect stderr, use defensive coding)
- [ ] Know how to interrupt (e.g., `pkill -f monitoring.sh`, or kill cron job)

---

## ✅ **IV. Bonus Part (Only if Mandatory is Perfect!)**

### 🔹 Advanced Partitioning
- [ ] Design nested LVM or multi-tier layout (e.g., `/`, `/var`, `/home`, `/srv`)
- [ ] Ensure no overlap, proper sizing (~500MB boot, 1–2GB swap, rest for LVs)

### 🔹 WordPress Stack
- [ ] Install and configure:
  - Web server: **lighttpd** (lean alternative to Apache/NGINX — *allowed*)
  - Database: **MariaDB**
  - Language: **PHP** (with modules: `php-mysql`, `php-cgi`, etc.)
- [ ] Secure installation:
  - Run DB setup (`mysql_secure_installation`)
  - Create DB/user for WordPress
  - Configure `lighttpd` → FastCGI with PHP
  - Download & configure WordPress (`wp-config.php`)
- [ ] Firewall update: open port `80` (or custom port), possibly `443` if TLS
- [ ] Optional: Let’s Encrypt for HTTPS (advanced)

### 🔹 Extra Service (Non-Apache/NGINX)
- [ ] Choose & deploy a *useful* service (e.g.):
  - `fail2ban` (intrusion prevention)
  - `rsyslog`/`syslog-ng` (advanced logging)
  - `postfix` (mail alerts for monitoring)
  - `grafana` + `node_exporter` (metrics dashboard)
  - `mosquitto` (MQTT for IoT)
- [ ] Justify choice during defense: why useful? security impact? resource use?

---

## ✅ **V. Documentation & Submission**

### 🔹 README.md
- [ ] First line: *italicized* — `*This project has been created as part of the 42 curriculum by <login>.*`
- [ ] Sections:
  - **Description**: goal, summary
  - **Instructions**: how to set up, run monitoring, log in
  - **Project Description**:
    - OS choice justification (Debian vs Rocky)
    - Design choices: partitioning, password/sudo/firewall policies
    - Comparison tables:
      - Debian ↔ Rocky
      - AppArmor ↔ SELinux
      - UFW ↔ firewalld
      - VirtualBox ↔ UTM
  - **Resources**: links (man pages, Debian Handbook, Rocky Docs, etc.)
  - **AI Usage Statement**: *exactly* how AI was used (e.g., “Clarified LUKS encryption syntax”, NOT “generated sudoers config”)

### 🔹 Submission
- [ ] Generate SHA1 of VM disk (`.vdi` or `.qcow2`)
- [ ] Save in `signature.txt`
- [ ] **DO NOT** commit VM files
- [ ] Test: `sha1sum <file>` matches `signature.txt`

---

## ✅ **VI. Defense Prep (Anticipate Questions!)**

- [ ] Practice explaining:
  - Why no GUI? Why encrypted LVM?
  - How your password policy is enforced
  - How sudo logging works (input/output capture)
  - SELinux/AppArmor modes & booleans used (if any)
  - How `monitoring.sh` computes CPU % or sudo count
  - How to stop `monitoring.sh` without editing script
- [ ] Be ready to:
  - Modify hostname during review
  - Create a new user + assign group
  - Add a firewall rule
  - Show `/etc/crypttab`, `/etc/fstab`, `/etc/sudoers`
  - Explain every line of monitoring script

