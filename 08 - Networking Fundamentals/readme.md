# Network Vulnerability Assessment Instructions

## Phase 1: "I'd like to Teach the World to Ping"

In this phase, I conducted a network assessment by pinging the network assets of RockStar Corp's Hollywood office to determine which IPs were accepting connections.

### Steps Taken
1. **Identify Hollywood Office IPs**: Identified the IP ranges associated with the Hollywood office:
   - 15.199.95.91/28
   - 15.199.94.91/28
   - 11.199.158.91/28
   - 167.172.144.11/32
   - 11.199.141.91/28
2. **Ping the IPs**: Used `fping` to ping the IP ranges from my local machine to determine which IPs were responsive:
   ```
   fping -g 15.199.95.91/28
   fping -g 15.199.94.91/28
   fping -g 11.199.158.91/28
   fping -g 167.172.144.11/32
   fping -g 11.199.141.91/28
   ```
   - Ignored results indicating "unreachable."
   - Only `167.172.144.11` responded, indicating that it was accepting connections.

### Summary of Results
- **Responsive IP**: `167.172.144.11` was the only IP that accepted connections.
- **OSI Layer Involved**: Network (Layer 3).

---

## Phase 2: "Some SYN for Nothin'"

With the responsive IP found in Phase 1, I proceeded to determine which ports were open using a SYN scan.

### Steps Taken
1. **SYN Scan**: Used Nmap to run a SYN scan against the IP address that was accepting connections:
   ```
   sudo nmap -sS 167.172.144.11
   ```
   - This scanned the most common 1000 ports to identify which ones were open.

### Summary of Results
- **Open Ports**: Only **port 22** (SSH) was found to be open.
- **OSI Layer Involved**: Transport (Layer 4).

---

## Phase 3: "I Feel a DNS Change Comin' On"

After identifying the open port, I attempted to log in to the server using default credentials to investigate potential DNS issues reported by RockStar Corp.

### Steps Taken
1. **Login Attempt**:
   - **Username**: `jimi`
   - **Password**: `hendrix`
   - Successfully logged in via SSH to the IP address `167.172.144.11` using the following command:
   ```
   ssh jimi@167.172.144.11 -p 22
   ```
2. **Check for DNS Issues**:
   - Navigated to the `/etc/hosts` file and found the following entry:
   ```
   98.137.246.8 rollingstone.com
   ```
   - This entry was causing DNS resolution issues for `rollingstone.com` in the Hollywood office.
3. **NSLookup**:
   - Used `nslookup` to determine the actual domain for the IP address found in the hosts file:
   ```
   nslookup 98.137.246.8
   ```
   - The lookup confirmed that the IP address was associated with a suspicious domain.

### Summary of Findings
- **DNS Manipulation**: The `/etc/hosts` file had been modified to redirect `rollingstone.com` to a different IP address.
- **OSI Layer Involved**: Application (Layer 7).

---

## Phase 4: "ShARP Dressed Man"

In this phase, I analyzed packet captures left by a hacker to determine any suspicious activity in the Hollywood office.

### Steps Taken
1. **Locate Packet Captures**: Found a note in the `/etc` directory indicating the location of packet captures:
   ```
   Captured Packets are here: https://drive.google.com/file/d/1ic-CFFGrbruloYrWaw3PvT71elTkh3eF/view?usp=sharing
   ```
2. **Wireshark Analysis**: Used Wireshark to analyze the downloaded PCAP file.
   - **Focus**: Focused on ARP and HTTP protocols to identify any unusual activity.

### Findings
- **ARP Spoofing**: Observed unusual ARP requests, indicating possible ARP spoofing attempts.
- **HTTP Requests**: Detected suspicious HTTP GET requests, suggesting unauthorized access or data exfiltration.
- **OSI Layers Involved**: Data Link (Layer 2) for ARP and Application (Layer 7) for HTTP.

---

## Quiz Questions & Answers

1. **Full command used to ping the 'Hollywood Web Server 2' machine**:
   - Answer: `ping 203.0.113.32`

2. **OSI layer involved in 'ping' commands**:
   - Answer: `Network`

3. **What is unique about a SYN scan?**:
   - Answer: `It never completes the three-way handshake`

4. **Nmap scan flag for a SYN scan**:
   - Answer: `nmap -sS`

5. **Port open on the IP address scanned via SYN scan**:
   - Answer: `Port 22`

6. **IP address obtained through viewing the /etc/hosts file**:
   - Answer: `98.137.246.8`

7. **Port left open by Rock Star**:
   - Answer: `Port 22`

8. **Hacker's device's MAC address**:
   - Answer: *(Pending Analysis)*

