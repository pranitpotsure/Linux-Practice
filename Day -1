
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
