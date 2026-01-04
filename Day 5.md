# DAY 5 – Networking (Linux Perspective)

## Objective
Understand **Linux networking fundamentals** and how traffic flows to and from a Linux server.
This knowledge is critical for debugging connectivity issues in DevOps and production environments.

This day focuses on:
- Network interfaces and IP addressing
- Open ports and listening services
- Network connectivity testing
- Understanding request flow to a Linux server

---

## Task 1: Network Interfaces

### View IP addresses and interfaces
```bash
ip a
```

Purpose:
- Shows all network interfaces
- Displays IP addresses (private/public)
- Helps identify active interfaces

---

## Task 2: Identify Open Ports

### View listening ports and services
```bash
ss -tuln
```

Explanation:
- `t` → TCP
- `u` → UDP
- `l` → Listening
- `n` → Numeric output

Purpose:
- Identify which services are exposed
- Verify application ports

---

## Task 3: Network Connectivity Testing

### Test basic connectivity
```bash
ping google.com
```

Purpose:
- Verifies network reachability
- Confirms outbound connectivity

---

### Test HTTP/HTTPS from CLI
```bash
curl http://example.com
```

```bash
curl https://example.com
```

Purpose:
- Tests application-level connectivity
- Verifies web servers and APIs

---

## Task 4: Trace Network Path

### Trace route to destination
```bash
traceroute google.com
```

Purpose:
- Shows hop-by-hop network path
- Helps identify network delays or blocks

---

## Practice Tasks

### Identify Open Ports on Server
```bash
ss -tuln
```

Look for:
- SSH port (22 or custom port like 2222)
- Web ports (80, 443)
- Application-specific ports

---

### Test Website from CLI
```bash
curl -I https://example.com
```

Purpose:
- Fetches HTTP headers
- Confirms server response status

---

## How a Request Reaches a Linux Server (Deliverable Notes)

### 1. DNS Resolution
- Client resolves domain name to IP address using DNS

### 2. Network Routing
- Request travels through routers and ISPs
- Firewalls and security groups filter traffic

### 3. Server Network Interface
- Packet reaches server’s network interface (NIC)
- IP address matches incoming request

### 4. Port and Service Check
- Linux kernel checks destination port
- Service must be listening on that port

### 5. Application Processing
- Web server or application processes request
- Generates response

### 6. Response Back to Client
- Response travels back through the same network path

---

## Why This Matters in DevOps
- Helps debug connectivity issues
- Essential for load balancers and reverse proxies
- Critical for cloud security and firewall rules
- Enables faster incident resolution

---

