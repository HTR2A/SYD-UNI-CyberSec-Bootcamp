# Defensive Security Solution for VSI

In this project, I acted as a Security Operations Center (SOC) analyst for Virtual Space Industries (VSI), a company specialising in virtual-reality programs for businesses. VSI faced a potential threat from a competitor, JobeCorp, that might be planning cyberattacks to disrupt our operations. Over two days, I was responsible for setting up and then evaluating a defensive solution using Splunk to monitor critical systems, including the Apache web server that hosts the administrative webpage and the Windows server running backend operations.

### **Presentation to Senior Management**
I compiled all my findings into a presentation for senior management, which can be accessed here: [Presentation](https://github.com/HTR2A/SYD-UNI-CyberSec-Bootcamp/blob/main/22%20-%20Building%20a%20Sec%20Monitoring%20Environment/JASON%20KING%20-%20Project%203%20Presentation.pdf)

### **Report for Senior Management and technical Staff**
The full report, which includes detailed analyses, screenshots of dashboards, and specific attack findings, can be accessed here: [Full Report](https://github.com/HTR2A/SYD-UNI-CyberSec-Bootcamp/blob/main/19%20-%20SIEMs/readme.md)

### **Day 1: Developing the Defensive Solution**

On Day 1, my objective was to build an effective monitoring solution to protect VSI’s systems. Here’s how I approached it:

1. **Loading and Analysing Historical Logs:**
   - I started by loading **Windows security logs** into Splunk, followed by **Apache web server logs**. These logs represented normal operational activity and served as the baseline for creating custom monitoring tools.
   - I thoroughly analysed these logs to gain a better understanding of VSI’s environment and the kind of activities occurring regularly. This allowed me to understand key metrics like login events, server errors, and HTTP requests.

2. **Creating Reports, Alerts, and Dashboards:**
   - **Reports:** I created several reports to assist in ongoing monitoring and to provide quick insights:
     - A **severity levels report** summarised the different severity levels of logged events in the Windows logs.
     - A report comparing **success and failure rates of activities** on the Windows server, which helped identify suspicious activity like repeated failed login attempts.
     - A report detailing **HTTP methods** such as GET and POST for Apache logs to provide insight into what kind of HTTP activities were being requested.
     - Reports on the **top referring domains** and **HTTP response codes** for Apache logs, which could help identify unusual web activity or signs of probing by attackers.
   - **Alerts:** I set up alerts based on baselines derived from historical data:
     - For the **Windows logs**, I created alerts for scenarios such as excessive **failed login attempts**, an unusual volume of **successful logins**, and any sudden rise in **deleted user accounts**.
     - For the **Apache logs**, I set up alerts for suspicious **international activity** from outside the typical customer regions and **high volume POST requests**, which could indicate attempts to exploit the system or upload malicious files.
   - **Dashboards:** I created two dashboards:
     - The **Windows Server Monitoring Dashboard** included visualisations to track signatures, user activities, and overall security events in real time.
     - The **Apache Web Server Monitoring Dashboard** showed patterns in HTTP methods, geographical distribution of clients, referrer domains, and URI access. This helped visualise ongoing access patterns and quickly spot irregularities.

3. **Installing Splunk Add-On for Enhanced Monitoring:**
   - I installed the **XML IP Geolocation API add-on** from Splunkbase, which enabled geographic monitoring by determining the geographical location of IP addresses from the logs. This added functionality was crucial to identifying anomalous geographic trends, such as sudden surges in traffic from unfamiliar regions. I provided an example scenario in which this add-on could help detect Distributed Denial of Service (DDoS) attacks.

4. **Establishing Baselines and Thresholds:**
   - I analysed the data to establish baselines of normal activity and set thresholds that would trigger alerts when exceeded. For instance, the baseline for failed logins was established at 5.91 per hour, and the alert was set to trigger at a threshold of 12. This avoided false positives while remaining sensitive enough to detect suspicious activity.

### **Day 2: Analysing Attacks and Evaluating the Solution**

On Day 2, I received logs detailing actual attacks on VSI’s systems—likely carried out by JobeCorp. The attacks targeted both the Windows and Apache servers that I had been monitoring. My task was to evaluate whether the monitoring solution I created on Day 1 had effectively captured these threats.

1. **Loading and Analysing Attack Logs:**
   - I uploaded new logs representing the attack period into Splunk. These included **Windows attack logs** and **Apache attack logs**.
   - I used the dashboards, alerts, and reports I previously created to analyse the data, compare it to baselines, and look for anomalies.

2. **Windows Logs Analysis:**
   - **Severity Levels:** The severity of logged events changed notably during the attack. High-severity incidents decreased from 93% to 79%, while low-severity events increased significantly, indicating a shift towards system misconfigurations or routine errors.
   - **Failed Activities:** A spike in failed activities was identified between 8 a.m. and 9 a.m. on March 25th, involving privileged actions like **password resets and account deletions**, pointing towards a targeted attack or insider threat.
   - **Suspicious User Activity:** I observed **196 successful logins attributed to User J** within an hour, which was highly unusual and suggested compromised credentials.
   - **Account Lockouts and Password Resets:** There was a sharp increase in **account lockouts and password reset attempts**, indicating coordinated efforts to compromise user accounts, particularly between midnight and 11 a.m.

3. **Apache Logs Analysis:**
   - **HTTP Methods and POST Requests:** During the attack, there was a dramatic rise in **HTTP POST requests**, increasing from 1% to 29%. POST requests are typically used to send data, and this suggested attempts to upload malicious files or exploit server-side vulnerabilities.
   - **HTTP Response Codes:** A significant increase in **404 errors** indicated that attackers were scanning the server for vulnerable or non-existent files, which was a sign of an attack attempt.
   - **Geographic Activity:** There was a notable spike in traffic from **Ukraine**, which was flagged as suspicious international activity. The number of events increased to 937 within an hour, raising concerns about potential distributed attacks originating from this region.

4. **Alert Analysis:**
   - The alerts I set on Day 1 for both Windows and Apache logs effectively captured the suspicious activities during the attack period:
     - The **Failed Logins Alert** was triggered due to the spike in failed login attempts.
     - The **Successful Logins Alert** flagged the unusual volume of logins attributed to User J, indicating possible credential compromise.
     - For Apache, the alert for **high HTTP POST activity** correctly identified the attack pattern, and the **non-US activity alert** caught the suspicious surge in Ukrainian traffic.

5. **Evaluation of Dashboards:**
   - The dashboards proved highly useful for visualising the attack data:
     - The **Windows Monitoring Dashboard** showed clear spikes in suspicious user activity and account lockouts.
     - The **Apache Monitoring Dashboard** revealed abnormal spikes in **HTTP methods** and geographical traffic, making it evident when and where the attacks were occurring.

### **Presentation to Senior Management**
I compiled all my findings into a presentation for senior management, which can be accessed here: [Presentation](https://github.com/HTR2A/SYD-UNI-CyberSec-Bootcamp/blob/main/22%20-%20Building%20a%20Sec%20Monitoring%20Environment/JASON%20KING%20-%20Project%203%20Presentation.pdf), detailing:
- **The attacks on VSI**: Summarising the incidents, including the spike in malicious activities like account lockouts, suspicious logins, and HTTP POST requests.
- **Effectiveness of Monitoring Solutions**: Demonstrating how the reports, alerts, and dashboards captured the anomalies and provided critical insights into attack patterns.
- **Key Findings and Mitigations**:
  - Suspicious activities on the **Windows server**, such as repeated password reset attempts and unauthorised logins.
  - On the **Apache server**, increased POST requests and traffic from unfamiliar regions.
  - Recommended mitigations included rate limiting, CAPTCHA or **Multi-Factor Authentication (MFA)** to prevent brute-force attacks, **geo-blocking** for high-risk regions, and enhanced monitoring of unusual user behaviours.

### **Summary and Future Mitigations**
The attack on VSI highlighted several vulnerabilities across both the Windows and Apache systems. Key mitigations include:
- Implementing **rate limiting** and **MFA** to reduce the risk of brute-force attacks.
- Strengthening **file upload mechanisms** and input validation to prevent malicious POST activity.
- **Geo-blocking** or increased monitoring of high-risk regions, especially given the spike in Ukrainian traffic.
- Regular **vulnerability scans** and **penetration testing** to preemptively discover weaknesses before attackers can exploit them.

The full report, which includes detailed analyses, screenshots of dashboards, and specific attack findings, can be accessed here: [Full Report](https://github.com/HTR2A/SYD-UNI-CyberSec-Bootcamp/blob/main/19%20-%20SIEMs/readme.md)

---

