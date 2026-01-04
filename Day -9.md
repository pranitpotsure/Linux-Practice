# DAY 9 – Server Hardening (Production Level)

## Objective
Apply **production-level server hardening practices** to reduce the attack surface of a Linux server.

This day focuses on:
- Firewall configuration
- Disabling unused services
- Verifying exposed ports
- Creating a security checklist

---

## Task 1: Firewall Setup (Linux)

### Check firewall status (firewalld)
```bash
sudo systemctl status firewalld
```

If not installed:
```bash
sudo dnf install -y firewalld
```

Start and enable firewall:
```bash
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

---

### Allow required ports only

#### Allow SSH (custom port example: 2222)
```bash
sudo firewall-cmd --permanent --add-port=2222/tcp
```

#### Allow HTTP & HTTPS (if required)
```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
```

Reload firewall:
```bash
sudo firewall-cmd --reload
```

Verify rules:
```bash
sudo firewall-cmd --list-all
```

---

## Task 2: Disable Unused Services

### List running services
```bash
systemctl list-units --type=service --state=running
```

### Disable unused service (example: postfix)
```bash
sudo systemctl stop postfix
sudo systemctl disable postfix
```

Verify:
```bash
systemctl status postfix
```

---

## Task 3: Verify Open Ports

### Check listening ports
```bash
ss -tuln
```

### Check ports with owning services
```bash
sudo ss -tulnp
```

Confirm:
- Only required ports are open
- No unexpected services are listening

---

## Security Checklist (Deliverable)

### SSH Hardening
- [ ] SSH key-based login enabled
- [ ] Password authentication disabled
- [ ] Root login disabled
- [ ] SSH running on non-default port

### Firewall
- [ ] Firewall enabled and running
- [ ] Only required ports allowed
- [ ] Default deny policy applied

### Services
- [ ] Unused services identified
- [ ] Unused services stopped and disabled
- [ ] Only required services running

### Networking
- [ ] Open ports verified
- [ ] No unnecessary public exposure
- [ ] Local-only services bound to 127.0.0.1

### Monitoring & Maintenance
- [ ] Logs reviewed regularly
- [ ] Disk usage monitored
- [ ] Cron jobs reviewed

---

## Why Server Hardening Matters
- Reduces attack surface
- Prevents unauthorized access
- Protects sensitive data
- Improves compliance and reliability

---
