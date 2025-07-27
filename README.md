# 🛰️ Task 1: Scan Your Local Network for Open Ports (Cybersecurity Internship)

## 🎯 Objective
Understand and apply basic **network reconnaissance** skills using **Nmap** to discover open ports on devices in your local network and analyze their potential risks.

---

## 🛠️ Tools Required
- **Nmap** (Install via Kali: `sudo apt install nmap`)
- **Wireshark** (Optional: Packet analysis)
- **Kali Linux Terminal**

---

## ✅ Step-by-Step Instructions

### 🔹 Step 1: Install Nmap
```bash
sudo apt update
sudo apt install nmap
```
Or download from: https://nmap.org/download.html

### 🔹 Step 2: Find Your IP Range
Run:
```bash
ip a
```
Look for your local IP (e.g., `192.168.1.7`) → calculate subnet range (e.g., `192.168.1.0/24`).

### 🔹 Step 3: Run a TCP SYN Scan
```bash
nmap -sS 192.168.1.0/24 -oN scan_results.txt
```
- `-sS`: TCP SYN scan (stealthy)
- `-oN`: Save output in normal format

📸 Save screenshot: `screenshots/nmap_scan.png`

### 🔹 Step 4: Analyze the Output
Example result:
```
Nmap scan report for 192.168.1.10
Host is up.
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
```

🔍 Interpretation:
- Port 22 → SSH → If open on a user machine, may allow brute-force.
- Port 80/443 → Web server running → Is it needed on this device?

---

## 🧪 Step 5 (Optional): Analyze Traffic with Wireshark
1. Open Wireshark.
2. Start capture on active interface.
3. Filter by:
```plaintext
ip.addr == 192.168.1.10
```
4. Observe SYN, SYN-ACK handshakes.
📸 Screenshot: `screenshots/wireshark_capture.png`

---

## 🚨 Common Services & Risk Table
| Port | Service | Risk |
|------|---------|------|
| 21   | FTP     | Unencrypted login data |
| 22   | SSH     | Brute-force attacks |
| 23   | Telnet  | Insecure protocol |
| 80   | HTTP    | Unencrypted traffic |
| 443  | HTTPS   | Safer, but misconfigurations possible |
| 3306 | MySQL   | Database exposure risk |

---

## 🔒 How to Secure Open Ports
- Close unused ports via firewall: `ufw` or `iptables`
- Use secure protocols (e.g., SSH instead of Telnet)
- Update and patch services regularly
- Use intrusion detection (Snort, Suricata)

---

## 📚 Key Concepts
- **Open Port:** A TCP/UDP port accepting connections
- **TCP SYN Scan:** Sends SYN packet, observes response without completing handshake
- **Network Reconnaissance:** Identifying devices and services
- **Firewall:** Blocks unauthorized access to/from network

---

## ❓ Interview Questions (with Answers)

### 1. What is an open port?
An open port is a network port that accepts incoming connections. Attackers scan for these to find vulnerabilities.

### 2. How does Nmap perform a TCP SYN scan?
It sends a SYN packet to target ports. If SYN-ACK is received, the port is open. It doesn’t complete the handshake, making it stealthy.

### 3. What risks are associated with open ports?
They expose services that might be unpatched or misconfigured, allowing exploitation, malware injection, or lateral movement.

### 4. Explain the difference between TCP and UDP scanning.
- **TCP scan:** Connection-oriented, receives acknowledgments.
- **UDP scan:** Connectionless, relies on ICMP "port unreachable" responses.

### 5. How can open ports be secured?
- Use firewalls
- Close unused ports
- Use encrypted and authenticated services

### 6. What is a firewall's role regarding ports?
It allows or blocks traffic on specific ports, acting as a gatekeeper to reduce attack surface.

### 7. What is a port scan and why do attackers perform it?
A method to discover open ports/services on a host. Used for reconnaissance before launching attacks.

### 8. How does Wireshark complement port scanning?
It visually analyzes packet exchanges. Helps verify traffic, detect anomalies, and validate scan activity (SYN/SYN-ACK packets).

---

## 📂 Recommended GitHub Repository Structure
```
network-scan-task/
├── README.md
├── scan_results.txt
├── screenshots/
│   ├── nmap_scan.png
│   └── wireshark_capture.png
```



## ✍️ Task Completed By:
**Nitin sanap **  
Cybersecurity Intern
