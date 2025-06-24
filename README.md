📌 Project Steps & Documentation
✅ 1. Install Nmap
Download and install Nmap from the official site:
👉 https://nmap.org/download.html

Verify installation by running:

bash
Copy
Edit
nmap -v
✅ 2. Find Your Local IP Range
Use the following command to identify your system’s local IP address:

Windows:
ipconfig

Linux/macOS:
ifconfig or ip a

Example output:

nginx
Copy
Edit
IPv4 Address: 192.168.1.105
Subnet Mask: 255.255.255.0
Based on this, the IP range is: 192.168.1.0/24

✅ 3. Run a TCP SYN Scan with Nmap
Run the following command to perform a TCP SYN scan:

bash
Copy
Edit
nmap -sS 192.168.1.0/24 -oN scan_output.txt -oX scan_output.xml
Explanation:

-sS: Stealth (SYN) scan.

192.168.1.0/24: Full local subnet.

-oN: Output in text format.

-oX: Output in XML format (useful for further analysis).

✅ 4. Note Down IPs & Open Ports
Sample Nmap output:

bash
Copy
Edit
Nmap scan report for 192.168.1.1
Open ports: 80/tcp, 443/tcp

Nmap scan report for 192.168.1.101
Open ports: 22/tcp, 139/tcp, 445/tcp
✅ 5. Analyze Packet Capture with Wireshark (Optional)
Wireshark Steps:

Start capture on your active network interface.

Run the Nmap scan while capture is active.

Apply this display filter to see SYN-ACK responses (open ports):

wireshark
Copy
Edit
tcp.flags.syn == 1 && tcp.flags.ack == 1
Save a screenshot or pcap file for documentation.

✅ 6. Research Common Services on Open Ports
Port	Protocol	Service	Description
22	TCP	SSH	Secure Shell - remote login
80	TCP	HTTP	Web server (insecure)
443	TCP	HTTPS	Secure web server
139	TCP	NetBIOS	File sharing on Windows
445	TCP	SMB	Windows file sharing & printers

✅ 7. Identify Security Risks from Open Ports
Findings from scan:

192.168.1.1 (Router)

Open Ports: 80, 443

🔒 Risk: Web admin page exposed. Ensure strong password, use HTTPS only.

192.168.1.101 (Workstation)

Open Ports: 22, 139, 445

🔒 Risks:

SSH (22): Brute-force attacks if default credentials are used.

SMB (445): Vulnerable to known exploits (e.g., EternalBlue).

NetBIOS (139): May leak information about shared folders.

✅ 8. Save the Scan Results
The results were saved in multiple formats:

scan_output.txt: Human-readable text format

scan_output.xml: XML format (for use in automation/reporting)

You can also generate HTML using:

bash
Copy
Edit
xsltproc scan_output.xml -o scan_output.html
