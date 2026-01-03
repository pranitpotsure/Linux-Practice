# DAY 3 – Processes, Services & Logs (Linux)

## Objective
Understand how Linux handles **processes, services, and logs**, and learn how to troubleshoot real production issues such as service failures.

This day focuses on:
- Process monitoring
- Service management with systemd
- Log analysis
- Incident troubleshooting workflow

---

## Task 1: Process Monitoring

### View running processes
```bash
ps aux
```

Explanation:
- Shows all running processes
- Includes CPU, memory usage, and owning user

---

### Real-time process monitoring
```bash
top
```

(Optional – better UI)
```bash
htop
```

---

## Task 2: Service Management

### Check SSH service status
```bash
systemctl status sshd
```

Important fields to observe:
- Active (running / failed)
- Loaded unit file
- Recent log messages

---

### Start SSH service
```bash
sudo systemctl start sshd
```

### Stop SSH service
```bash
sudo systemctl stop sshd
```

### Restart SSH service
```bash
sudo systemctl restart sshd
```

---

## Task 3: Log Analysis with journalctl

### View recent system errors
```bash
sudo journalctl -xe
```

### View logs for SSH service only
```bash
sudo journalctl -u sshd
```

---

## Task 4: Explore System Logs

### Authentication logs
```bash
sudo cat /var/log/auth.log
```

Purpose:
- SSH login attempts
- Authentication failures
- sudo usage

---

### System logs
```bash
sudo cat /var/log/syslog
```

Purpose:
- Kernel messages
- Service-level errors
- System events

---

## Failure Drill – SSH Service Down (CRITICAL PRACTICE)

### Step 1: Stop SSH service
```bash
sudo systemctl stop sshd
```

Confirm service is stopped:
```bash
systemctl status sshd
```

---

### Step 2: Attempt SSH login from new terminal
Expected result:
```text
Connection refused
```

---

### Step 3: Investigate Root Cause Using Logs

Check SSH logs:
```bash
sudo journalctl -u sshd
```

Check system error logs:
```bash
sudo journalctl -xe
```

---

### Step 4: Fix the Issue

Start SSH service:
```bash
sudo systemctl start sshd
```

Verify:
```bash
systemctl status sshd
```

---

## Incident Note – SSH Down (Deliverable)

### Incident Summary
SSH service was unreachable on the server.

### Impact
- Remote access to the server was unavailable.

### Root Cause
- SSH daemon (`sshd`) was stopped.

### Resolution
- Identified service state using `systemctl status`
- Analyzed logs using `journalctl`
- Restarted SSH service

### Preventive Measures
- Monitor critical services
- Enable alerts for service downtime
- Avoid accidental service stops

---

## Why This Matters in DevOps
- Production issues often start with service failure
- Logs are the primary source of truth
- Fast diagnosis reduces downtime
- Incident documentation improves reliability

---
