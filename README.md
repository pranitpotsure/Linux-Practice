# DAY 0 – Server & Mindset Setup (Linux + AWS)

## Objective
Set up a Linux server following **enterprise security best practices**:
- No direct root SSH access
- Personal user with sudo privileges
- SSH key–based authentication
- Proper permission hardening

This task focuses on **security-first mindset**, not tools.

---

## Environment
- Cloud: AWS EC2
- OS: Amazon Linux 2023
- Access: SSH (key-based)
- Local OS: Windows (PowerShell)

---

## Step 1: Launch EC2 Instance
- Created EC2 instance using Amazon Linux
- Downloaded SSH key pair (`devops.pem`)
- Configured Security Group to allow SSH (port 22)

---

## Step 2: Login to Server via SSH
```bash
ssh -i devops.pem ec2-user@<server_ip>
```
Verify session:

whoami
hostname
uptime

Step 3: Switch to Root (Temporary)
sudo su


Root access is used only for administrative setup, not daily work.

Step 4: Create Personal User
useradd pranit


(Optional password – not required for key-based login)

passwd pranit

Step 5: Configure SSH Access for Personal User
Create .ssh directory
mkdir -p /home/pranit/.ssh
chmod 700 /home/pranit/.ssh

Copy SSH public key
cp /home/ec2-user/.ssh/authorized_keys /home/pranit/.ssh/

Fix ownership & permissions
chmod 600 /home/pranit/.ssh/authorized_keys
chown -R pranit:pranit /home/pranit/.ssh

Step 6: Give Sudo Access (wheel group)

Amazon Linux controls sudo access using the wheel group.

usermod -aG wheel pranit


Verify:

groups pranit


Expected output:

pranit wheel

Step 7: Test Login as Personal User (MANDATORY)

Open a new terminal (do not logout existing session):

ssh -i devops.pem pranit@<server_ip>


Test sudo:

sudo whoami


Expected output:

root

Step 8: Disable Root SSH Login

Edit SSH configuration:

sudo vi /etc/ssh/sshd_config


Set (add or modify):

PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes


Restart SSH service:

sudo systemctl restart sshd

Step 9: Final Verification
Root login should FAIL
ssh root@<server_ip>

Personal user login should WORK
ssh pranit@<server_ip>
