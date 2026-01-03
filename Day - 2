# DAY 2 – Users, Groups & Access Control (Linux)

## Objective
Understand **Linux authentication, authorization, and access control**, which are foundational for secure server administration and DevOps practices.

This day focuses on:
- User and group management
- Access control via groups
- SSH security hardening
- Understanding how Linux authentication works

---

## Task 1: Create User

Create a new user for development purposes.

```bash
sudo useradd devuser
```

Set password for the user:

```bash
sudo passwd devuser
```

Verify user creation:

```bash
id devuser
```

---

## Task 2: Create Group

Create a group for DevOps engineers.

```bash
sudo groupadd devops
```

Verify group creation:

```bash
getent group devops
```

---

## Task 3: Add User to Group

Add `devuser` to the `devops` group.

```bash
sudo usermod -aG devops devuser
```

Verify group membership:

```bash
groups devuser
```

Expected output:
```text
devuser devops
```

---

## Task 4: Configure SSH Key-Based Login

### Step 1: Switch to devuser
```bash
su - devuser
```

### Step 2: Create `.ssh` directory
```bash
mkdir -p ~/.ssh
chmod 700 ~/.ssh
```

### Step 3: Add public key
Paste your SSH public key into `authorized_keys`.

```bash
vi ~/.ssh/authorized_keys
```

Set correct permissions:

```bash
chmod 600 ~/.ssh/authorized_keys
```

---

## Task 5: Change SSH Port (Security Hardening)

Edit SSH configuration file:

```bash
sudo vi /etc/ssh/sshd_config
```

Change default port:
```text
Port 2222
```

⚠️ Ensure your firewall / security group allows the new port before restarting SSH.

---

## Task 6: Restart SSH Safely

Always test configuration before restarting.

```bash
sudo sshd -t
```

If no errors, restart SSH service:

```bash
sudo systemctl restart sshd
```

---

## Verification

### Login using new SSH port
```bash
ssh -p 2222 devuser@<server_ip>
```

---

## How Linux Authentication Works (Deliverable Notes)

### 1. User Identity
- Users are defined in `/etc/passwd`
- Passwords are stored securely in `/etc/shadow`

### 2. Authentication
- SSH authenticates users via:
  - Passwords
  - SSH key pairs (public/private)
- SSH daemon (`sshd`) handles login requests

### 3. Authorization
- Groups define what users can access
- Group membership controls permissions on files and directories

### 4. Privilege Escalation
- `sudo` allows temporary root access
- Access controlled by `/etc/sudoers`

### 5. Access Control Layers
- File permissions (`rwx`)
- User and group ownership
- SSH configuration
- Firewall and network rules

---

## Why This Matters in DevOps
- Prevent unauthorized access
- Enforce least privilege
- Separate duties using groups
- Secure remote server access

---
