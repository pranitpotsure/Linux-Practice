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

