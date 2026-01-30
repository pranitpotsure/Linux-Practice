# Linux for DevOps & Cloud Engineering
_A Practical, Production-Oriented Guide_

---

## 1. Why Linux Is the Backbone of DevOps & Cloud

Linux is not just an operating system — it is the **foundation layer** on which modern DevOps, Cloud, and SRE practices are built.

### Why DevOps Runs on Linux
- Most cloud servers run Linux (AWS, Azure, GCP)
- All container technologies (Docker, Kubernetes) run natively on Linux
- Automation, CI/CD, monitoring, logging tools are Linux-first
- Open-source, stable, secure, and customizable
- Designed for multi-user, multi-process, networked environments

> If you understand Linux deeply, you can debug any DevOps issue, even when tools fail.

---

## 2. Linux in Real DevOps & Cloud Environments

Linux is used at every layer of DevOps:

| Layer | Linux Role |
|-----|-----------|
| Cloud VM | EC2, Compute Engine, Azure VM |
| Containers | Docker runtime, container OS |
| Orchestration | Kubernetes nodes |
| CI/CD | Jenkins, GitHub Actions runners |
| Monitoring | Prometheus, Grafana agents |
| Security | Firewall, SSH, IAM integration |
| Networking | Load balancers, proxies |
| Storage | Volumes, mounts, backups |

---

## 3. Linux Architecture (Core Components)

Linux is built in layers. Understanding these layers helps you troubleshoot from first principles.

### 3.1 Linux Kernel
Responsibilities:
- Process management
- Memory management
- Device drivers
- File system handling
- Networking

---

### 3.2 Shell (CLI Interface)

The shell is how DevOps engineers control servers.

Why CLI matters:
- Automation via scripts
- Remote server control
- Faster than GUI
- Required for production debugging

---

### 3.3 File System Hierarchy

| Directory | Purpose |
|--------|--------|
| / | Root |
| /etc | Config files |
| /var | Logs & runtime data |
| /opt | Applications |
| /home | User data |

---

## 4. Users, Groups & Permissions

Linux is multi-user by design.

- Users: /etc/passwd
- Groups: logical access control
- Permissions: rwx model

Example:
-rw-r----- pranit pranit secure.txt

---

## 5. SSH & Secure Access

Best practices:
- SSH key-based login
- Disable root login
- Disable password authentication
- Use sudo

---

## 6. Processes & Services (systemd)

Commands:
- ps aux
- top
- systemctl status/start/stop/restart

---

## 7. Logs & Troubleshooting

Important logs:
- journalctl
- /var/log/auth.log
- /var/log/syslog

---

## 8. Disk, Memory & Storage

Commands:
- df -h
- du -sh
- free -m

Disk full is a top cause of outages.

---

## 9. Networking (Linux Perspective)

Commands:
- ip a
- ss -tuln
- curl
- ping
- traceroute

---

## 10. Server Hardening

Checklist:
- Firewall enabled
- Required ports only
- Unused services disabled
- SSH hardened
- Logs monitored

---

## 11. Linux in DevOps Incident Handling

Incidents include:
- Disk full
- Service down
- Login failure

Linux enables fast diagnosis and recovery.

---

## 12. Final Takeaway

Linux is the backbone of DevOps and Cloud.
Master Linux → Master DevOps.
