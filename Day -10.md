# DAY 10 – Final Real-World DevOps Challenge

## Scenario
A production Linux server is facing multiple critical issues:

🚨 Disk Full  
🚨 Service Down  
🚨 User Login Failed  

This challenge simulates a **real on-call DevOps incident** where you must diagnose, fix, and document problems.

---

## Objective
- Identify issues using Linux commands
- Analyze logs to find root causes
- Fix the problems safely
- Document incidents professionally

---

## Issue 1: Disk Full

### Identification
```bash
df -h
```

### Investigation
```bash
du -sh /var/log/*
```

### Fix
```bash
sudo rm -rf /var/log/old_logs/*
```

### Verification
```bash
df -h
```

---

## Issue 2: Service Down (SSH Example)

### Identification
```bash
systemctl status sshd
```

### Logs
```bash
sudo journalctl -u sshd
```

### Fix
```bash
sudo systemctl start sshd
```

### Verification
```bash
systemctl status sshd
```

---

## Issue 3: User Login Failed

### Identification
```bash
sudo tail -n 50 /var/log/secure
```

### Common Causes
- Wrong permissions on `.ssh`
- SSH key missing
- Password authentication disabled

### Fix
```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

## Incident Documentation (MANDATORY)

For each issue, document:

- Incident summary
- Impact
- Root cause
- Resolution
- Preventive actions

---
