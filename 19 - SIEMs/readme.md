# Cybersecurity Module 19 Challenge Submission: Splunk Analysis Report

## Introduction
This report presents a detailed analysis of the Splunk investigation performed for the Module 19 challenge. The focus of this exercise was to identify cyberattacks, analyze system vulnerabilities, and develop mitigation strategies using Splunk as a monitoring tool. The report covers the identification of attack timelines, system recovery, vulnerability assessment, and baseline establishment for monitoring brute force attacks.

### Step 1: Incident Detection - The Need for Speed

#### 1. Attack Identification
The investigation revealed that the attack took place on **February 23, 2020, at approximately 2:30 PM GMT**. This was determined by analyzing the logs and identifying abnormal spikes in network activity and failed login attempts during that specific timeframe.

The attack vector was traced back to unauthorized access attempts targeting the organization's external-facing servers. The attackers exploited a known vulnerability in the web application, which allowed them to gain partial access to the system. The logs showed a series of failed login attempts followed by a successful breach, indicating a brute force attack method.

#### 2. System Recovery Duration
The recovery process took approximately **9 hours**. During this time, several critical actions were undertaken:

- **Incident Containment**: The affected systems were isolated to prevent the spread of the attack.
- **Root Cause Analysis**: Security analysts performed a root cause analysis to determine the exploit used by the attackers.
- **Patch Management**: The identified vulnerability was patched, and system configurations were updated to prevent similar breaches in the future.
- **System Restoration**: Backups were used to restore affected systems to their original state, and additional security measures were put in place to ensure system integrity.

#### Evidence
The report includes a screenshot of the Splunk dashboard that shows the timeline of the attack, highlighting the spike in malicious activity and the sequence of events leading to the breach.
![Screenshot 2024-09-27 at 15 26 16](https://github.com/user-attachments/assets/36fba758-18d2-4131-b860-5ed7fc253269)
![Screenshot 2024-09-27 at 16 33 30](https://github.com/user-attachments/assets/95a10da7-1598-41db-aab8-2b74c1460b96)

### Step 2: Assessing Vulnerabilities

In this phase, a thorough assessment of system vulnerabilities was conducted using Splunk's alerting capabilities. The objective was to create proactive monitoring rules that would help in early detection of similar threats in the future.

- **Vulnerability Identification**: Using Splunk, we analyzed historical data and identified patterns indicative of potential vulnerabilities, such as repeated failed login attempts and unusual IP addresses accessing the system.
- **Alert Configuration**: An alert was configured to monitor these patterns. Specifically, the alert was designed to trigger if failed login attempts exceeded the defined threshold, or if an IP address exhibited suspicious behavior such as multiple access attempts within a short period.

#### Evidence
Screenshots are provided to demonstrate the creation of the alert in Splunk. The screenshots include:

- **Alert Logic**: The logic used to define the alert, including the conditions set for failed login attempts and IP address monitoring.
- **Alert Trigger**: The configuration showing the actions taken when the alert is triggered, such as sending email notifications to the security team and logging the event for further analysis.
![Screenshot 2024-09-27 at 15 35 50](https://github.com/user-attachments/assets/18d9f520-1808-4abe-8b96-bac7ace57348)
![Screenshot 2024-09-27 at 15 38 12](https://github.com/user-attachments/assets/0563a105-fd67-4adf-a1f5-73c60a6e36d9)
![Screenshot 2024-09-27 at 15 44 41](https://github.com/user-attachments/assets/f7a0283e-ae3a-4df8-a454-58c84fd97453)
![Screenshot 2024-09-27 at 15 44 41](https://github.com/user-attachments/assets/c0cd907a-696e-4bb2-be54-b59a5ea7f8c7)
![Screenshot 2024-09-27 at 15 44 46](https://github.com/user-attachments/assets/58a34868-9da9-4687-9ef9-1d4f2305e687)
![Screenshot 2024-09-27 at 15 44 58](https://github.com/user-attachments/assets/4b1906ea-a35a-4be7-ae1f-69804c69c78f)
![Screenshot 2024-09-27 at 15 45 23](https://github.com/user-attachments/assets/27dc3e78-3ef3-419d-b3be-e9eeaabf0ca7)


### Step 3: Establishing a Baseline for Brute Force Attacks

#### 1. Timing of Brute Force Attack
A detailed analysis of the logs showed that a **brute force attack** occurred between **9:00 AM and 1:00 PM on Friday, February 21, 2020**. During this period, there were significant peaks in failed login attempts:

- **9:00 AM**: A total of **124 failed login events** were recorded.
- **1:00 PM**: A similar spike was observed, with **123 failed login events**.

These spikes were far above the normal baseline of failed login attempts and indicated an ongoing brute force attack, likely using automated scripts to attempt multiple password combinations.

#### 2. Baseline Activity and Alert Threshold
To establish a baseline for normal login activity, historical data from the system logs were analyzed. It was determined that the **normal baseline** for failed login attempts is around **15 per hour**. To minimize false positives while maintaining a proactive approach, the alert threshold was set at **18 failed login attempts per hour**.

This threshold was chosen based on the following considerations:

- **Minimizing False Positives**: Setting the threshold slightly above the baseline helps in avoiding unnecessary alerts due to occasional failed logins by legitimate users.
- **Proactive Threat Detection**: The threshold is low enough to detect brute force attacks early, giving the security team ample time to respond before any successful breach occurs.

#### Evidence
The evidence includes screenshots showing the following:

- **Baseline Analysis**: The analysis performed in Splunk to determine the normal login failure rate, including a graph that plots failed login attempts over time.
- **Alert Configuration**: The alert settings that specify the conditions under which the security team is notified of potential brute force activity.
![Screenshot 2024-09-27 at 15 50 22](https://github.com/user-attachments/assets/abde2179-23a0-4640-a324-5c64fbaec54f)
![Screenshot 2024-09-27 at 15 50 33](https://github.com/user-attachments/assets/32591847-21b0-4be7-86a2-8b415f02002e)
![Screenshot 2024-09-27 at 16 29 16](https://github.com/user-attachments/assets/442e4fbc-dd03-4cc3-958a-75401b24d844)
![Screenshot 2024-09-27 at 16 29 26](https://github.com/user-attachments/assets/e8519c11-576c-4c9b-9d3b-954218988649)
![Screenshot 2024-09-27 at 16 29 40](https://github.com/user-attachments/assets/b9fe5076-3086-49fa-98e8-c9632a300f48)
![Screenshot 2024-09-27 at 16 29 56](https://github.com/user-attachments/assets/eb4fcbb6-d043-4322-86eb-2e10ba7093be)
![Screenshot 2024-09-27 at 16 30 07](https://github.com/user-attachments/assets/10c88f0d-0f68-434d-9bdc-7bd412673793)


### Conclusion
This report provides a comprehensive analysis of the cybersecurity incident, detailing the attack timeline, recovery actions, vulnerability assessment, and proactive measures taken to mitigate future threats. By leveraging Splunk's monitoring capabilities, we were able to:

- **Identify Attack Timelines**: Pinpoint the exact date and time of the attack, allowing for a swift response.
- **Determine Recovery Measures**: Effectively contain and recover from the attack within a **9-hour** window.
- **Establish Monitoring Alerts**: Set up alerts based on historical data to detect future incidents, specifically targeting brute force attacks and suspicious activity.

The proactive use of Splunk as a monitoring tool has significantly improved our ability to detect, respond to, and prevent cybersecurity incidents. The detailed screenshots attached to this report further illustrate each step of the analysis, providing transparency and clarity on the actions taken.


