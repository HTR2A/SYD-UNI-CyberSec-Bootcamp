# Module 2 Challenge Submission: Assessing Security Culture

## Step 1: Measure and Set Goals

### Potential Security Risks of Allowing Employees to Access Work Information on Their Personal Devices

1. **Malware Infection**: Personal devices are often not maintained with the same level of security as company devices, making them vulnerable to malware attacks that could lead to sensitive company data being compromised.
2. **Phishing Attacks**: Employees may inadvertently access phishing links on personal devices, which could lead to compromised credentials and unauthorised access to the corporate network.
3. **Unauthorised Access to Sensitive Information**: The use of personal devices without adequate security controls increases the risk of unauthorised access, either by an external attacker or someone who may have temporary access to the employee's personal device (e.g., family members or friends).

Additional risks include:
- **Lack of Encryption**: Many personal devices may not have encryption enabled, putting sensitive information at risk if the device is lost or stolen.
- **Unsecure Applications**: Personal devices often have a range of non-business applications, which could introduce vulnerabilities if they are exploited.

### Preferred Employee Behaviour

- **Avoid Downloading Suspicious Email Attachments**: Employees should only download attachments from trusted and verified senders.
- **Continuous Education and Awareness**: Employees should be educated regularly on recognising threats such as phishing and social engineering.
- **Keep Software Updated**: Maintaining up-to-date software ensures that vulnerabilities are patched, reducing the risk of exploits.
- **Use Strong Authentication**: Employees should use Multi-Factor Authentication (MFA) whenever possible to add an additional layer of security.
- **Secure Device Settings**: Devices should be configured with appropriate security settings, such as strong passwords, biometric access, and encryption.
- **Segregate Personal and Business Data**: Ensure that personal and work data are stored separately on personal devices, preferably using containerisation solutions or Virtual Private Networks (VPN).
- **Avoid Public WiFi**: Employees should avoid using public WiFi for accessing work information unless connected via a secure VPN.

### Methods to Measure Non-Compliance

- **Penetration Testing by Third Parties**: Regular penetration testing (testing 25% of the organisation at a time) can provide insight into vulnerabilities and test employees' adherence to security protocols.
- **Surveys and Questionnaires**: Quarterly surveys can be used to gauge employee understanding of security policies and track their behaviour patterns.
- **Compliance Checks**: These can include verifying whether employees are keeping software updated and following security protocols.
- **Monitoring and Reporting**: Use security monitoring tools to identify instances of non-compliance, such as accessing sensitive data over public networks or failing to use MFA.

### Organisational Goals

- **High Compliance with Security Policies**: Strive for consistent adherence to all security protocols.
- **Suspicious Attachment Downloads**: Reduce downloads of suspicious email attachments to less than 5% across the organisation.
- **Password Updates and MFA Usage**: Ensure that passwords are updated regularly and that MFA usage reaches 100%.
- **Public WiFi Usage**: Aim to have less than 5% of employees using public WiFi without a secure VPN.
- **Training Frequency**: Conduct regular security awareness training for all employees.

## Step 2: Involve the Right People

### Key Employees or Departments Involved

- **CISO (Chief Information Security Officer)**: Oversees the organisation's cybersecurity strategy and the enforcement of BYOD policies. Ensures that employees are aware of security best practices and that robust policies are in place to mitigate risks.
- **IT Department**: Responsible for setting up and maintaining the technical controls required for a secure BYOD environment. This includes configuring secure network access, managing device enrolment, and deploying Mobile Device Management (MDM) tools.
- **HR Department**: Integrates security awareness into employee onboarding, ensuring that employees understand their responsibilities regarding company data. HR is also involved in ongoing training and reinforcing the importance of cybersecurity compliance.
- **Compliance and Legal Team**: Ensures all security measures comply with data protection laws (e.g., GDPR) and internal policies. They also assess the legal implications of BYOD and advise on privacy matters.
- **Department Heads/Managers**: Managers are key to fostering a security-conscious culture within their teams. They reinforce adherence to security policies, report non-compliance, and ensure that employees have access to the necessary resources and training.

## Step 3: Training Plan

### Training Frequency and Format

- **Frequency**: Training should occur during onboarding, every three months, and on an ad-hoc basis when significant changes or incidents occur.
- **Format**: The training should be a combination of in-person and online formats to accommodate different learning styles. In-person sessions can be more interactive, while online modules allow for self-paced learning.

### Training Topics

1. **Importance of Cybersecurity**: Explain why cybersecurity is crucial, the potential risks to both the company and the individual, and how a breach could impact employment.
2. **Keeping Software and Applications Up to Date**: Stress the importance of keeping devices updated to protect against known vulnerabilities.
3. **Authentication Measures**: Train on creating strong passwords, using password managers, and the importance of enabling Multi-Factor Authentication (MFA).
4. **Device Security Settings**: Show employees how to configure their devices securely, including using encryption and enabling secure backups.
5. **Data Segregation**: Educate employees on separating personal and work-related data to minimise risk.
6. **Public WiFi Dangers**: Warn employees about the dangers of using unsecured networks and teach them how to use VPNs when on public WiFi.
7. **Data Protection and Privacy**: Highlight the principles of data protection and how employees can ensure compliance.
8. **Safe Web Browsing Practices**: Teach employees how to identify secure websites, avoid clicking on suspicious links, and use ad-blockers.
9. **Incident Reporting and Response**: Outline how to recognise and report security incidents, and what steps they should take if they suspect a breach.
10. **Social Engineering Awareness**: Explain common social engineering tactics, such as phishing and pretexting, and how to avoid falling victim.

### Measuring Training Effectiveness

- **Penetration Testing**: Use penetration testing to identify whether employees are adhering to security policies in practice.
- **Surveys and Questionnaires**: Conduct these to evaluate employees' understanding of key concepts covered in the training.
- **Compliance Audits**: Assess whether employees follow established security practices, such as MFA usage and avoiding public WiFi.
- **Monitoring Employee Behaviour**: Analyse employee actions over time to see if there’s an increase in compliance and a decrease in risky behaviour.

## Bonus: Other Solutions

### Mobile Device Management (MDM)
- **Control Type**: Technical
- **Goal**: Preventive, Detective, Corrective
- **Advantage**: MDM allows for centralised control over employee devices, enforcing security policies, managing updates, and wiping devices remotely if needed.
- **Disadvantage**: Cost can be a significant barrier, especially for smaller organisations, and it may lead to privacy concerns from employees.

### Endpoint Detection and Response (EDR)
- **Control Type**: Technical
- **Goal**: Preventive, Detective, Corrective
- **Advantage**: EDR solutions provide continuous monitoring and analysis to detect, respond to, and mitigate endpoint threats, improving overall security.
- **Disadvantage**: Complexity of implementation and managing alerts can be challenging, requiring dedicated personnel or a Security Operations Centre (SOC).

### Network Segmentation
- **Control Type**: Technical
- **Goal**: Preventive
- **Advantage**: Segmentation reduces the attack surface by isolating sensitive data from less secure parts of the network.
- **Disadvantage**: Implementation can be complex and may require restructuring existing network architecture.

