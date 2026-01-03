# DAY 0 – Server & Mindset Setup (Linux + AWS)

## Objective
Set up a Linux server following **enterprise security best practices**:
- No direct root SSH access
- Personal user with sudo privileges
- SSH key-based authentication
- Proper permission hardening

This day focuses on building a **security-first DevOps mindset** before installing any tools.

---

## Step 1: Verify Server Session
After logging into the server, verify basic session details.

```bash
whoami
hostname
uptime
```

---

## Step 2: Switch to Root (Temporary)
Switch to root user only for administrative setup.

```bash
sudo su
```

Root access is used **only for administrative configuration**, not daily work.

---

## Step 3: Create Personal User
Create a personal Linux user for daily operations.

```bash
useradd pranit
```

(Optional: Set password — not required for SSH key-based login)

```bash
passwd pranit
```

---

## Step 4: Configure SSH Access for Personal User

### Create `.ssh` directory
```bash
mkdir -p /home/pranit/.ssh
chmod 700 /home/pranit/.ssh
```

### Copy SSH public key
```bash
cp /home/ec2-user/.ssh/authorized_keys /home/pranit/.ssh/
```

### Fix ownership and permissions
```bash
chmod 600 /home/pranit/.ssh/authorized_keys
chown -R pranit:pranit /home/pranit/.ssh
```

---

## Step 5: Give Sudo Access (wheel group)
Amazon Linux controls sudo access using the **wheel** group.

```bash
usermod -aG wheel pranit
```

### Verify group membership
```bash
groups pranit
```

Expected output:
```text
pranit wheel
```

---

## Step 6: Test Login as Personal User (MANDATORY)
Open a **new terminal** (do NOT logout the existing session).

```bash
ssh -i devops.pem pranit@<server_ip>
```

### Test sudo access
```bash
sudo whoami
```

Expected output:
```text
root
```

---

## Step 7: Disable Root SSH Login
Edit the SSH configuration file.

```bash
sudo vi /etc/ssh/sshd_config
```

Set or modify the following values:

```text
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
```

Restart the SSH service to apply changes.

```bash
sudo systemctl restart sshd
```

---

## Step 8: Final Verification

### Root login should FAIL
```bash
ssh root@<server_ip>
```

### Personal user login should WORK
```bash
ssh pranit@<server_ip>
```

---

## Why Root Login Is Dangerous
- Root has unlimited system privileges
- No accountability or audit trail
- High risk of accidental system damage
- First target for brute-force attacks
- Violates the principle of least privilege

# DAY 1 – File System & Permissions (Linux)

## Objective
Understand the Linux filesystem hierarchy and **file permissions**, which are critical for security and daily DevOps operations.

This day focuses on:
- Directory structure creation
- File ownership and permissions
- Understanding `rwx`, `chmod`, `chown`, and `umask`

---

## Task 1: Create Directory Structure

Create the following directory structure:

```
/opt/devops-lab/
 ├── scripts/
 ├── logs/
 ├── backups/
```

### Commands Used
```bash
sudo mkdir -p /opt/devops-lab/{scripts,logs,backups}
```

### Verify Structure
```bash
ls -la /opt/devops-lab
```

---

## Task 2: Practice File System Commands

### List files with permissions
```bash
ls -la
```

### Change file permissions
```bash
chmod 755 filename
chmod 644 filename
```

### Change file ownership
```bash
sudo chown user:group filename
```

### View detailed file information
```bash
stat filename
```

### Check default permission mask
```bash
umask
```

---

## Challenge Task: Create Secure File

### Requirement
Create a file with:
- **Owner:** read & write
- **Group:** read only
- **Others:** no access

### Step 1: Create File
```bash
touch secure.txt
```

### Step 2: Set Ownership
```bash
sudo chown pranit:pranit secure.txt
```

### Step 3: Set Permissions
```bash
chmod 640 secure.txt
```

### Step 4: Verify
```bash
ls -l secure.txt
```

Expected output:
```text
-rw-r----- 1 pranit pranit secure.txt
```

---

## Understanding File Permissions (rwx)

| Symbol | Meaning | Value |
|------|--------|-------|
| r | read | 4 |
| w | write | 2 |
| x | execute | 1 |

### Permission Breakdown
- **Owner** permissions come first
- **Group** permissions come second
- **Others** permissions come last

---

## 755 vs 644 (Very Important)

### Permission 755
```text
rwx r-x r-x
```
- Owner: read, write, execute
- Group: read, execute
- Others: read, execute
- Common for: **scripts and directories**

### Permission 644
```text
rw- r-- r--
```
- Owner: read, write
- Group: read
- Others: read
- Common for: **configuration and text files**

---

## Why Permissions Matter in DevOps
- Prevent unauthorized access
- Protect sensitive files (logs, secrets, configs)
- Avoid accidental deletion or modification
- Enforce least privilege principle

---

