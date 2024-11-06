# Cybersecurity Bootcamp - Module 11: Network Security Challenge

## Part 1: Review Questions

### Security Control Types
1. **Walls, bollards, fences, guard dogs, cameras, and lighting**:
   - **Type**: Physical Controls. These controls protect the physical infrastructure and assets.

2. **Security awareness programs, BYOD policies, and ethical hiring practices**:
   - **Type**: Administrative Controls. These include policies and procedures that guide individuals' actions.

3. **Encryption, biometric fingerprint readers, firewalls, endpoint security, and intrusion detection systems**:
   - **Type**: Technical Controls. Technological measures used to protect information systems and data.

### Intrusion Detection and Attack Indicators
1. **Difference between IDS and IPS**:
   - **IDS (Intrusion Detection System)** monitors network traffic for suspicious activity and issues alerts.
   - **IPS (Intrusion Prevention System)** also monitors network traffic but takes action to block or prevent suspicious activity.

2. **Difference between IOA and IOC**:
   - **Indicator of Attack (IOA)**: Refers to behaviors indicating an attacker is attempting or planning an attack (present-focused).
   - **Indicator of Compromise (IOC)**: Refers to artifacts left behind after a breach has occurred (past-focused).

### The Cyber Kill Chain
1. **Reconnaissance**: The attacker gathers information about the target (e.g., finding employees on LinkedIn).
2. **Weaponization**: Creating a malicious payload (e.g., embedding malware into a PDF).
3. **Delivery**: Sending the malicious payload to the victim (e.g., via phishing email).
4. **Exploitation**: The victim opens the attachment, and the vulnerability is exploited.
5. **Installation**: The payload installs malware on the victim's system.
6. **Command and Control (C2)**: The malware establishes a connection to the attacker’s server.
7. **Actions on Objectives**: The attacker performs tasks, such as data exfiltration.

### Snort Rule Analysis

#### Snort Rule #1
- **Rule**: `alert tcp $EXTERNAL_NET any -> $HOME_NET 5800:5820 (msg:"ET SCAN Potential VNC Scan 5800-5820"; flags:S,12; threshold: type both, track by_src, count 5, seconds 60; reference:url,doc.emergingthreats.net/2002910; classtype:attempted-recon; sid:2002910; rev:5; metadata:created_at 2010_07_30, updated_at 2010_07_30;)`
  - **Explanation**: Alerts on TCP traffic from any external IP to internal IPs on ports 5800-5820 if SYN flags are observed 5 times within 60 seconds. Indicates a potential VNC scan.
  - **Kill Chain Stage**: Reconnaissance
  - **Attack Type**: VNC Scan

#### Snort Rule #2
- **Rule**: `alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any (msg:"ET POLICY PE EXE or DLL Windows file download HTTP"; flow:established,to_client; flowbits:isnotset,ET.http.binary; flowbits:isnotset,ET.INFO.WindowsUpdate; file_data; content:"MZ"; within:2; byte_jump:4,58,relative,little; content:"PE|00 00|"; distance:-64; within:4; flowbits:set,ET.http.binary; metadata: former_category POLICY; reference:url,doc.emergingthreats.net/bin/view/Main/2018959; classtype:policy-violation; sid:2018959; rev:4; metadata:created_at 2014_08_19, updated_at 2017_02_01;)`
  - **Explanation**: Alerts on HTTP traffic involving the download of Windows executable files by monitoring specific headers ("MZ" and "PE").
  - **Kill Chain Stage**: Delivery
  - **Attack Type**: Potential download of PE EXE or DLL Windows files

#### Snort Rule #3
- **Created Rule**:
  ```
  alert tcp $EXTERNAL_NET any -> $HOME_NET 4444 (msg:"Inbound traffic on port 4444 detected"; sid:1000001; rev:1;)
  ```
  - **Explanation**: This rule detects inbound TCP traffic on port 4444, which could be used for unauthorized remote control.

## Part 2: "Drop Zone" Lab

### Lab Setup and Configuration

1. **Remove UFW**:
   - **Command**:
     ```bash
     sudo apt-get remove ufw
     ```

2. **Enable and Start Firewalld**:
   - **Commands**:
     ```bash
     sudo systemctl enable firewalld
     sudo systemctl start firewalld
     sudo systemctl status firewalld
     ```

3. **List All Firewall Rules**:
   - **Command**:
     ```bash
     sudo firewall-cmd --list-all
     ```

4. **List Supported Services**:
   - **Command**:
     ```bash
     sudo firewall-cmd --get-services
     ```

5. **List All Configured Zones**:
   - **Command**:
     ```bash
     sudo firewall-cmd --get-zones
     ```

6. **Create Zones (Web, Sales, Mail)**:
   - **Commands**:
     ```bash
     sudo firewall-cmd --permanent --new-zone=web
     sudo firewall-cmd --permanent --new-zone=sales
     sudo firewall-cmd --permanent --new-zone=mail
     sudo firewall-cmd --reload
     ```

7. **Assign Interfaces to Zones**:
   - **Commands**:
     ```bash
     sudo firewall-cmd --permanent --zone=public --change-interface=eth0
     sudo firewall-cmd --permanent --zone=web --change-interface=eth1
     sudo firewall-cmd --permanent --zone=sales --change-interface=eth2
     sudo firewall-cmd --permanent --zone=mail --change-interface=eth3
     sudo firewall-cmd --reload
     ```

8. **Add Services to Zones**:
   - **Public Zone**:
     ```bash
     sudo firewall-cmd --zone=public --add-service=http --permanent
     sudo firewall-cmd --zone=public --add-service=https --permanent
     sudo firewall-cmd --zone=public --add-service=pop3 --permanent
     sudo firewall-cmd --zone=public --add-service=smtp --permanent
     ```
   - **Web Zone**:
     ```bash
     sudo firewall-cmd --zone=web --add-source=201.45.34.126 --permanent
     sudo firewall-cmd --zone=web --add-service=http --permanent
     ```
   - **Sales Zone**:
     ```bash
     sudo firewall-cmd --zone=sales --add-source=201.45.15.48 --permanent
     sudo firewall-cmd --zone=sales --add-service=https --permanent
     ```
   - **Mail Zone**:
     ```bash
     sudo firewall-cmd --zone=mail --add-source=201.45.105.12 --permanent
     sudo firewall-cmd --zone=mail --add-service=smtp --permanent
     sudo firewall-cmd --zone=mail --add-service=pop3 --permanent
     ```

9. **Add Blacklisted IPs to Drop Zone**:
   - **Command**:
     ```bash
     sudo firewall-cmd --permanent --zone=drop --add-source=10.208.56.23
     sudo firewall-cmd --permanent --zone=drop --add-source=135.95.103.76
     sudo firewall-cmd --permanent --zone=drop --add-source=76.34.169.118
     sudo firewall-cmd --reload
     ```

10. **Block Specific IP and ICMP Requests**:
    - **Block IP 138.138.0.3 in Public Zone**:
      ```bash
      sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="138.138.0.3" drop' --permanent
      sudo firewall-cmd --reload
      ```
    - **Block ICMP Echo Requests**:
      ```bash
      sudo firewall-cmd --zone=public --add-icmp-block=echo-request --permanent
      sudo firewall-cmd --reload
      ```

## Part 3: IDS, IPS, DiD, and Firewalls

### IDS vs IPS Systems
1. **Two Ways an IDS Connects to a Network**:
   - **Port Mirror**
   - **Network Tap**

2. **How an IPS Connects to a Network**:
   - **Inline Deployment**

3. **Signature-based IDS**: Compares traffic patterns to predefined signatures.

4. **Anomaly-based IDS**: Detects deviations from a known baseline, useful for probing/sweeps.

### Defense in Depth Scenarios
1. **Physical Layer**: Tailgating through an exterior door.
2. **Application Layer**: Zero-day undetected by antivirus.
3. **Database Layer**: Successful access to HR’s database.
4. **Host/System Layer**: Exploiting an OS vulnerability.
5. **Network Layer**: DDoS attack taking down a government website.
6. **Data Layer**: Misclassified data.
7. **Perimeter Layer**: Firewalking to produce a list of active services.

### Firewall Architectures and Methodologies
1. **Stateful Firewall**: Verifies the three-way TCP handshake.
2. **Stateful Inspection Firewall**: Considers entire connections, not just individual packets.
3. **Proxy Firewall**: Intercepts all traffic before forwarding it.
4. **Packet Filtering Firewall**: Examines source/destination IP without opening the packet.
5. **MAC Layer Firewall**: Filters based on MAC addresses.

