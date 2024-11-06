# Module 14 - Project 1 Submission

## Project 1: Technical Brief

**Web Application URL**: [https://jasonkingcyber.com.au](https://jasonkingcyber.com.au) (Now deleted)

<img width="713" alt="Screenshot 2024-11-06 at 15 45 06" src="https://github.com/user-attachments/assets/64592df9-e2e8-48d3-ba51-07091f73dc47">
<img width="631" alt="Screenshot 2024-11-06 at 15 45 16" src="https://github.com/user-attachments/assets/f7ecc529-1d55-4d1c-9c8a-063228c99d8d">
<img width="634" alt="Screenshot 2024-11-06 at 16 02 03" src="https://github.com/user-attachments/assets/bc3d1d4f-6ab4-439f-a65e-4841f8aea06c">

### Day 1 Questions

**Domain Selection**

1. **Domain Provider**: GoDaddy
2. **Domain Name**: jasonkingcyber.com.au

**Networking Questions**

1. **IP Address of Webpage**: 20.211.64.24
2. **Location of IP Address**: Sydney, NSW, Australia
3. **DNS Lookup and NS Record**:
   - The DNS lookup for "jasonkingcyber.com.au" returned the IP address 20.211.64.24. The NS record identifies the authoritative name servers responsible for the domain.

**Web Development Questions**

1. **Runtime Stack**: PHP 8.2 (Back-end)
2. **Assets Directory Content**: The `/var/www/html/assets` directory contained CSS files for styling the website and images used across the site. These are used for the front end.
3. **Front-end vs Back-end**: The contents of the assets directory (CSS & images) are related to the front end.

### Day 2 Questions

**Cloud Questions**

1. **Cloud Tenant**: A cloud tenant is a distinct entity, like an individual or organization, subscribing to cloud services, while ensuring complete data isolation from other tenants within the shared infrastructure.
2. **Importance of Access Policy on Key Vault**: Access policies in the key vault determine who can access, manage, and control sensitive keys, secrets, and certificates, thereby securing them against unauthorized access.
3. **Keys, Secrets, Certificates**:
   - **Keys**: Used for encryption and signing operations.
   - **Secrets**: Store sensitive information such as passwords.
   - **Certificates**: Verify the identity of a domain or entity.

**Cryptography Questions**

1. **Advantages of a Self-signed Certificate**: Self-signed certificates are cost-effective and easy to generate, which makes them ideal for internal testing environments where browser trust is not a primary concern.
2. **Disadvantages of a Self-signed Certificate**:
   - Lack of third-party verification, leading to potential security warnings for users.
   - Lack of trust by public browsers, which means that users see security warnings, making it unsuitable for public-facing websites.
3. **Wildcard Certificate**: A wildcard certificate is a type of SSL/TLS certificate that uses a wildcard character (\*) to secure multiple subdomains under the same domain. For instance, it allows securing subdomains such as "mail.jasonkingcyber.com.au" and "store.jasonkingcyber.com.au" using a single certificate. This reduces costs and simplifies management.
4. **TLS Versions on Azure**: SSL 3.0 is no longer supported due to security vulnerabilities, such as the POODLE attack, which can be used to decrypt sensitive information. TLS versions 1.0, 1.1, and 1.2 are provided by Azure as they offer stronger encryption and better security.

**SSL Certificate Questions**

1. **Is Your Browser Returning an Error for SSL Certificate?**: Yes, initially the browser returned an error because the self-signed certificate was not trusted by default.
2. **Validity of SSL Certificate**: 15/08/2024 - 16/02/2025
3. **Intermediate Certificate**: No intermediate certificate was found for the current setup.
4. **Root Certificate**: Yes, the root certificate is issued by a trusted certificate authority that verifies the authenticity of the website.
5. **Root Certificate in Browser Root Store**: Yes, the Chrome root store contains the certificates that Chrome trusts by default.
6. **Another Root CA in Browser's Root Store**: DigiCert Global Root CA

### Day 3 Questions

**Cloud Security Questions**

1. **Azure Web Application Gateway vs. Azure Front Door**:

   - **Azure Web Application Gateway**: Primarily used for managing regional traffic within a specific Azure region, focusing on security and monitoring.
   - **Azure Front Door**: A global service that routes and optimizes traffic across multiple regions, offering features such as global load balancing and CDN capabilities.

2. **SSL Offloading**:

   - **Definition**: SSL offloading is the process of handling SSL encryption and decryption on a dedicated device, such as a load balancer, rather than on web servers.
   - **Benefits**:
     - **Improved Performance**: Reduces workload on web servers, enabling them to handle more requests.
     - **Simplified Management**: Centralizes SSL certificate management for easier updates.
     - **Enhanced Security**: Dedicated devices can be optimized for secure encryption.

3. **WAF OSI Layer**: A Web Application Firewall (WAF) works at **Layer 7** of the OSI model (Application Layer).

4. **WAF Managed Rule: SQL Injection**: SQL injection involves inserting malicious SQL queries into input fields to manipulate or access databases, which can lead to unauthorized access or data breaches.

5. **SQL Injection Vulnerability Impact**: Without protection like Azure Front Door, the website could be vulnerable to SQL injection attacks. Attackers could exploit input fields to gain unauthorized access to databases.

6. **Custom WAF Rule - Blocking Traffic from Canada**: Yes, blocking all traffic from Canada would generally prevent users from accessing the site. However, users could bypass this restriction using VPNs or proxy servers, masking their true location.

### Disclaimer on Future Charges

- **Maintaining Website**: YES

I am aware that I am responsible for any charges that I incur by maintaining my website. I have reviewed the guidance for minimizing costs and monitoring Azure charges.

*(Please ensure to delete all project resources if you decide not to maintain the website to avoid unnecessary charges.)*

