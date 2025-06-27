# 🌐 DevOps Networking Readme: Commands, Concepts, and Scripts

This README consolidates fundamental networking concepts, practical bash commands, and troubleshooting scripts that are essential for DevOps and SRE professionals.

---

## 📘 Core Networking Concepts

Below is a comprehensive breakdown of fundamental networking concepts that every DevOps or Observability Engineer should understand deeply. These concepts are not only crucial in interviews but also for designing, debugging, and maintaining robust systems in production environments.

### 1. OSI Model (7 Layers)

The OSI (Open Systems Interconnection) model is a conceptual framework used to understand and standardize how different networking protocols interact in a network.

* **L1 - Physical Layer:** Deals with the physical transmission of data over network media like cables, switches, electrical signals. (e.g., Ethernet cables, fiber optics)
* **L2 - Data Link Layer:** Handles node-to-node data transfer and error detection using MAC addresses. (e.g., Switches, ARP protocol)
* **L3 - Network Layer:** Responsible for packet forwarding, including routing via IP addresses. (e.g., Routers, IP protocol)
* **L4 - Transport Layer:** Manages reliable data transfer and error recovery using TCP/UDP. (e.g., Ports, TCP retransmission)
* **L5 - Session Layer:** Establishes, manages, and terminates sessions. (e.g., APIs, socket sessions)
* **L6 - Presentation Layer:** Translates data formats like encryption and encoding. (e.g., SSL/TLS encryption)
* **L7 - Application Layer:** Closest to the user; protocols like HTTP, FTP, DNS operate here.

Understanding the OSI model helps isolate where a network issue is occurring during troubleshooting.

### 2. IP Addressing

Every device on a network is assigned an IP (Internet Protocol) address which uniquely identifies it.

* **IPv4:** 32-bit addresses written as 4 octets (e.g., 192.168.1.1). Limited to \~4.3 billion addresses.
* **IPv6:** 128-bit addresses written as hexadecimal (e.g., 2001:0db8::1). Vast address space.
* **CIDR Notation:** Classless Inter-Domain Routing; represents IP + subnet. For example, `192.168.1.0/24` means subnet mask 255.255.255.0.

Key commands:

```bash
ip addr show       # Show assigned IP addresses
hostname -I        # Show IPs assigned to the host
```

### 3. Subnetting

Subnetting divides a large network into smaller, manageable sub-networks. This increases efficiency and enhances security.

* Helps reduce network congestion
* Isolates network segments
* Ensures better IP address utilization

Example:

* Network: 192.168.1.0/24 → can be divided into two subnets:

  * 192.168.1.0/25 (first 128 addresses)
  * 192.168.1.128/25 (last 128 addresses)

Tool:

```bash
ipcalc 192.168.1.0/24  # View subnet info
```

### 4. Routing

Routing is the process of forwarding packets from one network to another using routers. It ensures communication between different subnets and networks.

* **Static Routing:** Manually configured routes using fixed paths. Simple but not scalable.
* **Dynamic Routing:** Uses protocols like BGP, OSPF to discover and adapt to the network changes.

Commands:

```bash
ip route            # Show routing table
route -n            # Show static routes
```

Use-case: If packets aren't reaching the destination, a routing issue is likely the cause.

### 5. DNS (Domain Name System)

DNS translates human-friendly domain names (like `openai.com`) into IP addresses (like `104.18.12.58`).

Common tools:

```bash
nslookup google.com    # Basic DNS query
dig openai.com +short  # Advanced DNS resolution
host github.com        # Reverse lookup
```

Troubleshooting DNS:

* Check `/etc/resolv.conf`
* Use alternate resolvers: 8.8.8.8 (Google), 1.1.1.1 (Cloudflare)

### 6. NAT (Network Address Translation)

NAT enables multiple devices with private IPs to share a single public IP when accessing the internet.

* **SNAT:** Source NAT, used for outgoing traffic
* **DNAT:** Destination NAT, used for incoming requests (e.g., port forwarding)

Used heavily in:

* Home routers
* Kubernetes (ClusterIP, NodePort)
* Cloud firewalls (AWS NAT Gateway)

Command to view NAT rules:

```bash
sudo iptables -t nat -L -n -v
```

### 7. Firewalls & Ports

Firewalls control traffic flow based on rules (IP, port, protocol).

* **iptables:** Low-level rule management (Linux)
* **ufw:** Simpler interface over iptables
* **AWS Security Groups:** Cloud firewall

Example:

```bash
sudo ufw status
sudo iptables -L -n
```

Common Ports:

* 22: SSH
* 80: HTTP
* 443: HTTPS
* 53: DNS
* 3306: MySQL

### 8. TCP vs UDP

These are Layer 4 (Transport Layer) protocols.

* **TCP (Transmission Control Protocol):**

  * Connection-oriented
  * Reliable (acknowledgements, retransmissions)
  * Used for SSH, HTTP(S), FTP

* **UDP (User Datagram Protocol):**

  * Connectionless
  * Faster, but no reliability guarantees
  * Used for DNS, video streaming, gaming

### 9. Tools & Commands

A list of essential Linux networking tools:

* `ping`: Test reachability to another host
* `traceroute`: Shows route path and latency
* `netstat` / `ss`: List open ports and connections
* `nc` (netcat): Port scanning, banner grabbing
* `tcpdump`: Packet capture (advanced)
* `nmap`: Network scanner
* `ip`, `ifconfig`: Interface and routing info
* `dig`, `host`, `nslookup`: DNS troubleshooting

Example:

```bash
ip addr show           # Show IPs
ss -tuln               # List open ports
tcpdump -i eth0 port 80  # Capture HTTP traffic
```

* `ping`, `traceroute`, `netstat`, `ss`, `nc`, `tcpdump`, `iftop`, `ip`, `ifconfig`, `nmap`

---

## ⚙️ Useful Bash Networking Scripts

### 1. Ping Test Script

```bash
#!/bin/bash
HOST="google.com"
ping -c 4 $HOST
```

### 2. Check Port Status

```bash
#!/bin/bash
PORT=22
HOST="127.0.0.1"
nc -zv $HOST $PORT
```

### 3. Display All Network Interfaces

```bash
#!/bin/bash
ip addr show
```

### 4. List All Listening Ports

```bash
#!/bin/bash
ss -tuln
```

### 5. Check Internet Connectivity

```bash
#!/bin/bash
ping -c 1 8.8.8.8 &> /dev/null && echo "Online" || echo "Offline"
```

### 6. Traceroute Script

```bash
#!/bin/bash
traceroute google.com
```

### 7. DNS Lookup Script

```bash
#!/bin/bash
dig openai.com +short
```

### 8. Get Public IP

```bash
#!/bin/bash
curl -s ifconfig.me
```

---

## 🧪 Real-Time Troubleshooting Scenarios

### ❗ Issue: Port not reachable

* ✅ **Check service:** `systemctl status <service>`
* ✅ **Check port:** `ss -tuln | grep <port>`
* ✅ **Check firewall:** `ufw status` / `iptables -L`
* ✅ **Check container:** `docker inspect <container>`

### ❗ Issue: No Internet Access

* ✅ `ping 8.8.8.8` vs `ping google.com` (check DNS)
* ✅ Check default route: `ip route`
* ✅ Check interface status: `ip link show`

### ❗ Issue: DNS Failure

* ✅ Check `/etc/resolv.conf`
* ✅ Use `dig`, `nslookup`
* ✅ Restart `systemd-resolved`

### ❗ Issue: Slow Network in Pod (K8s)

* ✅ Check CNI plugin status
* ✅ Use `kubectl exec` to `ping` from pod
* ✅ Validate `iptables` and `network policies`

---

## 📄 References

* [Networking Fundamentals - Cisco Docs](https://www.cisco.com)
* `man ping`, `man ip`, `man ss`, `man tcpdump`
