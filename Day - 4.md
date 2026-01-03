# DAY 4 – Disk, Memory & Storage (Linux)

## Objective
Understand how Linux manages **disk, memory, and storage**, and learn how to identify and troubleshoot disk-related issues that commonly cause server outages.

This day focuses on:
- Disk usage monitoring
- Storage devices and mounts
- Memory utilization
- Real-world disk failure scenarios

---

## Task 1: Check Disk Usage

### View disk usage by filesystem
```bash
df -h
```

Purpose:
- Shows total disk size
- Used and available space
- Helps identify full disks

---

### Find directory-wise disk usage
```bash
du -sh *
```

Purpose:
- Identifies which directories consume the most space

---

## Task 2: View Block Devices

### List disks and partitions
```bash
lsblk
```

Purpose:
- Shows disks, partitions, and mount points
- Helps understand storage layout

---

## Task 3: Check Mounted Filesystems

```bash
mount
```

Purpose:
- Displays all mounted filesystems
- Useful for troubleshooting missing mounts

---

## Task 4: Check Memory Usage

```bash
free -m
```

Purpose:
- Shows RAM usage in MB
- Helps identify memory pressure

---

## Challenge Tasks

### Find the Largest Directory
```bash
du -h / | sort -hr | head -10
```

---

### Check for Disk Usage Above 80%
```bash
df -h | awk '$5+0 > 80 {print $0}'
```

Purpose:
- Identifies filesystems nearing full capacity

---

## Why Disk Full Crashes Servers (Deliverable Notes)

### 1. Applications Cannot Write Data
- Logs cannot be written
- Databases fail to store transactions

### 2. System Services Fail
- Package managers break
- Temporary files cannot be created

### 3. Performance Degradation
- Excessive I/O wait
- Application timeouts

### 4. System Instability
- Services crash unexpectedly
- SSH login may fail

### 5. Recovery Becomes Difficult
- No space to write logs for debugging
- Cleanup becomes risky

---

## Real DevOps Practices
- Monitor disk usage continuously
- Set alerts at 70–80% usage
- Rotate logs using `logrotate`
- Clean unused files and backups

---
