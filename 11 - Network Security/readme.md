# Cybersecurity Bootcamp - Module 11: Network Security Report

## Overview

This report presents my findings and configurations from Module 11: Network Security. The aim was to demonstrate my ability to configure firewalls, understand Intrusion Detection and Prevention Systems, and apply the concepts of defense in depth. Below is a detailed outline of the activities completed, highlighting successes and areas for improvement based on the feedback provided.

## Firewalld Configuration

### Overview

For this module, I used **firewalld** as the main firewall management tool, transitioning from **ufw**. This included verifying that no instances of `ufw` were running to avoid conflicts. I then enabled and started `firewalld`, configuring it to run upon system boot. This ensures consistent protection after any system restart.

**: Below is a screenshot showing the verification process for `ufw` being disabled and transitioning to `firewalld`.

<img width="1107" alt="1" src="https://github.com/user-attachments/assets/7f22b970-f9d3-410b-9e1e-a0a6fa510b6b">


### Steps Taken

1. **Confirm Firewalld is Running**

   - Commands used to enable and start `firewalld`:

   ```bash
   sudo systemctl enable firewalld
   sudo systemctl start firewalld
   sudo systemctl status firewalld
   ```

   - **Expected Output**:

   ```
   ● firewalld.service - firewalld - dynamic firewall daemon
      Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor preset: enabled)
      Active: active (running)
   ```

   **: The following screenshot shows the successful activation of `firewalld`.

<img width="1043" alt="3" src="https://github.com/user-attachments/assets/3ba098df-4874-46c1-8ecc-13ea68602d72">


3. **List Firewall Rules**

   - **Command**: `sudo firewall-cmd --list-all`
   - The rules are verified to understand what configurations exist, preventing duplication and aiding further setup.

4. **Configure Zones**

   - Created zones for **web**, **sales**, and **mail** to segregate services logically.
   - Commands used:

   ```bash
   sudo firewall-cmd --permanent --new-zone=web
   sudo firewall-cmd --permanent --new-zone=sales
   sudo firewall-cmd --permanent --new-zone=mail
   sudo firewall-cmd --reload
   ```

5. **Assign Interfaces to Zones**

   - Commands used to assign interfaces to the designated zones:

   ```bash
   sudo firewall-cmd --permanent --zone=public --change-interface=eth0
   sudo firewall-cmd --permanent --zone=web --change-interface=eth1
   sudo firewall-cmd --permanent --zone=sales --change-interface=eth2
   sudo firewall-cmd --permanent --zone=mail --change-interface=eth3
   sudo firewall-cmd --reload
   ```

   **: Below is a screenshot demonstrating the assignment of interfaces to their respective zones.

 <img width="961" alt="2" src="https://github.com/user-attachments/assets/63542e0e-b601-42b0-9e28-5aaf6dcaae09">
  

7. **Add Services to Zones**

   - Commands used to add services such as **HTTP**, **HTTPS**, **SMTP**, and **POP3** to respective zones:
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

8. **Add Blacklisted IPs to Drop Zone**

   - **Command**:

   ```bash
   firewall-cmd --permanent --zone=drop --add-source=10.208.56.23
   firewall-cmd --permanent --zone=drop --add-source=135.95.103.76
   firewall-cmd --permanent --zone=drop --add-source=76.34.169.118
   firewall-cmd --reload
   ```

9. **Reload Configurations**

   - Command used to reload and write configurations to memory, ensuring persistence:

   ```bash
   sudo firewall-cmd --reload
   ```

## Snort Rules Analysis

### Rule #1 Breakdown

- **Snort Rule**:
  ```
  alert tcp $EXTERNAL_NET any -> $HOME_NET 5800:5820 (msg:"ET SCAN Potential VNC Scan 5800-5820"; flags:S,12; threshold: type both, track by_src, count 5, seconds 60; reference:url,doc.emergingthreats.net/2002910; classtype:attempted-recon; sid:2002910; rev:5; metadata:created_at 2010_07_30, updated_at 2010_07_30;)
  ```
- **Explanation**: Alerts on TCP traffic from any external IP to any internal IP on ports 5800 to 5820, monitoring SYN flags. If five attempts occur within 60 seconds, it triggers an alert indicating a potential VNC scan.
- **Cyber Kill Chain Stage**: Reconnaissance
- **Type of Attack**: Potential VNC Scan

### Custom Snort Rule

- **Created Rule**:
  ```
  alert tcp $EXTERNAL_NET any -> $HOME_NET 4444 (msg:"Inbound traffic on port 4444 detected"; sid:1000001)
  ```
- **Purpose**: To detect inbound traffic on port 4444, which may indicate a known malware backdoor attempt.

## Cyber Kill Chain

### Stages with Examples

1. **Reconnaissance**: Attacker searches LinkedIn to find employees of the targeted company, then uses Google dorks to find server vulnerabilities.
2. **Weaponization**: Creation of a malware payload to exploit CVE-2021-12345 vulnerability.
3. **Delivery**: Sending the malware as an attachment in a phishing email to the target.
4. **Exploitation**: Victim opens the attachment, exploiting the vulnerability and executing the payload.
5. **Installation**: The payload installs a backdoor (RAT) on the target's system.
6. **Command and Control (C2)**: Attacker establishes a connection with the backdoor for remote access.
7. **Actions on Objectives**: The attacker moves laterally across the network to exfiltrate sensitive data.

## IDS vs IPS Systems

| Feature             | IDS                         | IPS                                    |
| ------------------- | --------------------------- | -------------------------------------- |
| **Connection Type** | Port Mirror or Network Tap  | Inline                                 |
| **Action Taken**    | Detects and Alerts          | Detects and Blocks                     |
| **Best Use Case**   | Monitor and analyze traffic | Prevent malicious traffic in real-time |

- **Example of Signature-based IDS**: Ideal for comparing network patterns against predefined signatures; useful for detecting well-known attacks but ineffective against zero-day exploits.
- **Example of Anomaly-based IDS**: Detects deviations from the baseline network activity, capable of identifying unusual probing activities that do not match known signatures.

## Defense in Depth (DiD)

### Scenarios with Examples

1. **Physical Layer**: An attacker tailgates an employee through an exterior door into a secure facility.
2. **Application Layer**: A zero-day goes undetected by antivirus software.
3. **Host/System Layer**: An attacker exploits a vulnerability in the operating system.
4. **Network Layer**: A hacktivist successfully conducts a DDoS attack on a government website.
5. **Data Layer**: Sensitive data is misclassified, leading to unintended exposure.

## Firewall Architectures and Methodologies

| Firewall Type           | Description                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------- |
| **Packet Filtering**    | Examines packets at the network layer, filtering based on source/destination IP, port, and protocol. |
| **Stateful Inspection** | Considers the state of the connection, validating packets are part of an established session.        |
| **Proxy Firewall**      | Intercepts traffic and acts as an intermediary between source and destination, enhancing security.   |
| **MAC Layer Firewall**  | Filters packets based solely on MAC address, used for internal network segmentation.                 |

## Improvements Made

- Added examples to the **Cyber Kill Chain** stages to illustrate each step more comprehensively.
- Expanded on the differences between **IDS** and **IPS**, providing use cases and scenarios where one is preferable over the other.
- Improved the **firewalld** configuration section by adding details about listing rules and viewing active zones for greater clarity.

## Conclusion

This module provided hands-on experience in configuring a secure network environment using `firewalld`, analyzing network traffic with Snort rules, and understanding critical security concepts such as defense in depth. The feedback received helped refine key areas, ensuring a more complete understanding of firewall and IDS/IPS deployments.

Further steps will involve practising advanced firewall configurations and simulating more complex intrusion scenarios to enhance detection capabilities and response protocols.

