# Module 14 - Project 1 Submission

## Project 1: Technical Brief

**Web Application URL**: [https://jasonkingcyber.com.au](https://jasonkingcyber.com.au) (Now deleted)

### Screenshots of Website

<img width="713" alt="Screenshot 2024-11-06 at 15 45 06" src="https://github.com/user-attachments/assets/64592df9-e2e8-48d3-ba51-07091f73dc47">
<img width="631" alt="Screenshot 2024-11-06 at 15 45 16" src="https://github.com/user-attachments/assets/f7ecc529-1d55-4d1c-9c8a-063228c99d8d">
<img width="634" alt="Screenshot 2024-11-06 at 16 02 03" src="https://github.com/user-attachments/assets/bc3d1d4f-6ab4-439f-a65e-4841f8aea06c">

### Day 1 Questions

**Domain Selection**

1. **What domain provider did you use to purchase your domain?**
   - **Answer**: GoDaddy

2. **What is the domain name you have registered?**
   - **Answer**: jasonkingcyber.com.au

**Networking Questions**

1. **What is the IP address of your webpage?**
   - **Answer**: 20.211.64.24

2. **Where is the IP address location?**
   - **Answer**: Sydney, NSW, Australia

3. **What does a DNS lookup return and what is an NS record?**
   - **Answer**: The DNS lookup for "jasonkingcyber.com.au" returned the IP address 20.211.64.24. The NS record identifies the authoritative name servers responsible for the domain.

**Web Development Questions**

1. **What is the runtime stack for your web server?**
   - **Answer**: PHP 8.2 (Back-end)

2. **What content is in your assets directory and how is it used?**
   - **Answer**: The `/var/www/html/assets` directory contained CSS files for styling the website and images used across the site. These are used for the front end.

3. **Is the content in your assets directory related to the front end or back end?**
   - **Answer**: The contents of the assets directory (CSS & images) are related to the front end.

### Day 2 Questions

**Cloud Questions**

1. **What is a cloud tenant?**
   - **Answer**: A cloud tenant is a distinct entity, like an individual or organization, subscribing to cloud services, while ensuring complete data isolation from other tenants within the shared infrastructure.

2. **Why is an access policy important for a key vault?**
   - **Answer**: Access policies in the key vault determine who can access, manage, and control sensitive keys, secrets, and certificates, thereby securing them against unauthorized access.

3. **What is the difference between keys, secrets, and certificates?**
   - **Answer**: 
     - **Keys**: Used for encryption and signing operations.
     - **Secrets**: Store sensitive information such as passwords.
     - **Certificates**: Verify the identity of a domain or entity.

**Cryptography Questions**

1. **What are the advantages of a self-signed certificate?**
   - **Answer**: Self-signed certificates are cost-effective and easy to generate, which makes them ideal for internal testing environments where browser trust is not a primary concern.

2. **What are the disadvantages of a self-signed certificate?**
   - **Answer**:
     - Lack of third-party verification, leading to potential security warnings for users.
     - Lack of trust by public browsers, which means that users see security warnings, making it unsuitable for public-facing websites.

3. **What is a wildcard certificate?**
   - **Answer**: A wildcard certificate is a type of SSL/TLS certificate that uses a wildcard character (\*) to secure multiple subdomains under the same domain. For instance, it allows securing subdomains such as "mail.jasonkingcyber.com.au" and "store.jasonkingcyber.com.au" using a single certificate. This reduces costs and simplifies management.

4. **Why are certain TLS versions provided by Azure while SSL 3.0 is not?**
   - **Answer**: SSL 3.0 is no longer supported due to security vulnerabilities, such as the POODLE attack, which can be used to decrypt sensitive information. TLS versions 1.0, 1.1, and 1.2 are provided by Azure as they offer stronger encryption and better security.

**SSL Certificate Questions**

1. **Is your browser returning an error for your SSL certificate? Why or why not?**
   - **Answer**: Yes, initially the browser returned an error because the self-signed certificate was not trusted by default.

2. **What is the validity period of your SSL certificate?**
   - **Answer**: 15/08/2024 - 16/02/2025

3. **Do you have an intermediate certificate? If so, what is it?**
   - **Answer**: No intermediate certificate was found for the current setup.

4. **Do you have a root certificate? If so, what is it?**
   - **Answer**: Yes, the root certificate is issued by a trusted certificate authority that verifies the authenticity of the website.

5. **Does your browser have the root certificate in its root store?**
   - **Answer**: Yes, the Chrome root store contains the certificates that Chrome trusts by default.

6. **List one other root CA in your browser's root store.**
   - **Answer**: DigiCert Global Root CA

### Day 3 Questions

**Cloud Security Questions**

1. **What is the difference between Azure Web Application Gateway and Azure Front Door?**
   - **Answer**:
     - **Azure Web Application Gateway**: Primarily used for managing regional traffic within a specific Azure region, focusing on security and monitoring.
     - **Azure Front Door**: A global service that routes and optimizes traffic across multiple regions, offering features such as global load balancing and CDN capabilities.

2. **What is SSL offloading and what are its benefits?**
   - **Answer**:
     - **Definition**: SSL offloading is the process of handling SSL encryption and decryption on a dedicated device, such as a load balancer, rather than on web servers.
     - **Benefits**:
       - **Improved Performance**: Reduces workload on web servers, enabling them to handle more requests.
       - **Simplified Management**: Centralizes SSL certificate management for easier updates.
       - **Enhanced Security**: Dedicated devices can be optimized for secure encryption.

3. **At what OSI layer does a WAF work?**
   - **Answer**: A Web Application Firewall (WAF) works at **Layer 7** of the OSI model (Application Layer).

4. **What is a WAF managed rule for SQL injection?**
   - **Answer**: SQL injection involves inserting malicious SQL queries into input fields to manipulate or access databases, which can lead to unauthorized access or data breaches.

5. **What is the impact of a SQL injection vulnerability?**
   - **Answer**: Without protecti
