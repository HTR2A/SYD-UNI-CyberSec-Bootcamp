## Module 9: Networking Fundamentals II

### Mission 1: Mail Server Issues

**Issue**: With the DoS attack, the Empire took down the Resistance's DNS and primary email servers.

- **New Mail Servers**: The new primary mail server is `asltx.1.google.com`, and the secondary mail server should be `asltx.2.google.com`.
- **Current Situation**: The Resistance (starwars.com) can send emails but cannot receive any.

**Solution**:

- **Determine Mail Servers for `starwars.com`**:
  - **Command Used**:
    ```
    nslookup -type=mx starwars.com
    ```
  - **Output**: The MX records retrieved showed different servers from those intended (`asltx.1.google.com` and `asltx.2.google.com` were not found).

**Explanation**: The Resistance isn't receiving emails because the specified mail servers (`asltx.1.google.com` and `asltx.2.google.com`) do not exist (NXDOMAIN). The current DNS configuration points to other Google mail servers.

**Suggested DNS Corrections**:
1. **Use Valid Existing Mail Servers**: Update MX records to use valid mail servers (e.g., Google's).
2. **Verify DNS Propagation**: Ensure updated MX records have propagated correctly.
3. **Check Mail Server Connectivity**: Use `telnet` to verify mail server reachability on port 25.

---

### Mission 2: SPF Record Update

**Issue**: Users reported not receiving email alerts from `theforce.net`.

- **Current Situation**: The mail server's IP address for `theforce.net` changed, but the SPF record wasn't updated, causing emails to be marked as spam.

**Solution**:

- **Determine SPF Record for `theforce.net`**:
  - **Command Used**:
    ```
    nslookup -type=txt theforce.net
    ```
  - **Output**: The SPF record is:
    ```
    v=spf1 a mx a:mail.wise-advice.com mx:smtp.secureserver.net include:aspmx.googlemail.com ip4:45.63.15.159 ip4:45.63.4.215 ~all
    ```

**Explanation**: Emails were going to spam due to a soft fail (`~all`) and the absence of the new IP address (`45.23.176.21`) in the SPF record.

**Suggested DNS Corrections**:
1. **Add the New IP Address to SPF**: Include `45.23.176.21` to ensure emails from this IP are authorized.
2. **Change `~all` to `-all`**: Enforce stricter SPF policies to prevent unauthorized senders.

**Verification Steps**:
1. **Check Updated SPF Record**:
    ```
    nslookup -query=txt theforce.net
    ```
2. **Send Test Emails**: Ensure emails are delivered to the inbox.

---

### Mission 3: CNAME Record Correction

**Issue**: The subpage `resistance.theforce.net` is not redirecting to `theforce.net`.

**Solution**:

- **Determine CNAME for `www.theforce.net`**:
  - **Command Used**:
    ```
    nslookup -type=cname www.theforce.net
    ```
  - **Output**: `www.theforce.net` is a CNAME pointing to `theforce.net`.

**Explanation**: The subdomain `resistance.theforce.net` isn't redirecting because no CNAME record exists, resulting in an NXDOMAIN error.

**Suggested DNS Corrections**:
1. **Create CNAME Record for `resistance.theforce.net`**: Point `resistance.theforce.net` and `www.resistance.theforce.net` to `theforce.net`.

**Verification Steps**:
1. **Check Updated CNAME Records**:
    ```
    nslookup -type=cname resistance.theforce.net
    ```
2. **Test Redirection**: Confirm that the subpages redirect properly.

---

### Mission 4: Add Backup DNS Server

**Issue**: The primary DNS server of `princessleia.site` was taken down during the attack. The backup DNS server `ns2.galaxybackup.com` is not listed.

**Solution**:

- **Determine NS Records for `princessleia.site`**:
  - **Command Used**:
    ```
    nslookup -type=ns princessleia.site
    ```
  - **Output**: Current name servers are `ns25.domaincontrol.com` and `ns26.domaincontrol.com`.

**Suggested DNS Corrections**:
1. **Add `ns2.galaxybackup.com` as a Backup NS**: Ensure redundancy and prevent future downtime.

**Verification Steps**:
1. **Check Updated NS Records**:
    ```
    nslookup -type=ns princessleia.site
    ```
2. **Use Online DNS Propagation Checkers**: Verify changes have propagated.

---

### Mission 5: Optimizing Network Path from Batuu to Jedha

**Issue**: Network traffic from Batuu to Jedha is slow due to an attack on Planet N.

**Solution**:

- **Determine OSPF Shortest Path**:
  - **Shortest Path**: Batuu > D > C > E > F > J > I > L > Q > T > V > Jedha

**Verification**: Ensure that Planet N is not included in the route to optimize traffic.

---

### Mission 6: Decrypting Dark Side Wireless Traffic

**Issue**: Gather secret information from the Dark Side's encrypted wireless internet traffic.

**Solution**:

- **Use Aircrack-ng to Crack Wireless Key**:
  - **Command Used**:
    ```
    aircrack-ng -w rockyou.txt darkside_capture.pcap
    ```
- **Decrypted Information**:
  - **Device**: IP Address: `172.16.0.101`, MAC Address: `XX:XX:XX:55:98:ef`
  - **Router/Gateway**: IP Address: `172.16.0.1`, MAC Address: `00:0f:66:e3:e4:01`

---

### Mission 7: Hidden Message Retrieval

**Issue**: The Resistance wants to send you a secret message.

**Solution**:

- **Access the Hidden Message**:
  - **Command Used**:
    ```
    telnet towel.blinkenlights.nl
    ```

- **Verification**: Follow the instructions provided in the message to complete the mission.

---

