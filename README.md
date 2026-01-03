
```md
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
Step 2: Switch to Root (Temporary)
Switch to root user only for administrative setup.

bash
Copy code
sudo su
Root access is used only for administrative configuration, not daily work.

Step 3: Create Personal User
Create a personal Linux user for daily operations.

bash
Copy code
useradd pranit
(Optional: Set password — not required for SSH key-based login)

bash
Copy code
passwd pranit
Step 4: Configure SSH Access for Personal User
Create .ssh directory
bash
Copy code
mkdir -p /home/pranit/.ssh
chmod 700 /home/pranit/.ssh
Copy SSH public key
bash
Copy code
cp /home/ec2-user/.ssh/authorized_keys /home/pranit/.ssh/
Fix ownership and permissions
bash
Copy code
chmod 600 /home/pranit/.ssh/authorized_keys
chown -R pranit:pranit /home/pranit/.ssh
Step 5: Give Sudo Access (wheel group)
Amazon Linux controls sudo access using the wheel group.

bash
Copy code
usermod -aG wheel pranit
Verify group membership
bash
Copy code
groups pranit
Expected output:

text
Copy code
pranit wheel
Step 6: Test Login as Personal User (MANDATORY)
Open a new terminal (do NOT logout the existing session).

bash
Copy code
ssh -i devops.pem pranit@<server_ip>
Test sudo access
bash
Copy code
sudo whoami
Expected output:

text
Copy code
root
Step 7: Disable Root SSH Login
Edit the SSH configuration file.

bash
Copy code
sudo vi /etc/ssh/sshd_config
Set or modify the following values:

text
Copy code
PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes
Restart the SSH service to apply changes.

bash
Copy code
sudo systemctl restart sshd
Step 8: Final Verification
Root login should FAIL
bash
Copy code
ssh root@<server_ip>
Personal user login should WORK
bash
Copy code
ssh pranit@<server_ip>
Why Root Login Is Dangerous
Root has unlimited system privileges

No accountability or audit trail

High risk of accidental system damage

First target for brute-force attacks

Violates the principle of least privilege

Outcome
Secure SSH access using key-based authentication

Personal user with controlled sudo privileges

Root SSH login disabled

Enterprise-level Linux server hardening completed

Next Steps
DAY 1: Linux filesystem and permissions

Advanced SSH hardening

User and group management

Production Linux troubleshooting

Author: Pranit Potsure
Track: DevOps / Cloud Engineering

yaml
Copy code

---

## 🧠 WHY THIS FIX WORKS
- No commands outside code blocks
- No inline shell commands
- Clean Markdown hierarchy
- GitHub renderer stays consistent

---

## ✅ Final Checklist for Future `.md` Files
✔ Use `##` for steps  
✔ Use `###` for sub-steps  
✔ **Every command inside ```bash**  
✔ Never mix text + command on same line  

---

If you want next:
- 📁 `DAY-1-Linux-Filesystem.md`
- 📘 Professional `README.md` for whole repo
- 🧠 Interview-ready documentation style

Just tell me 👍
