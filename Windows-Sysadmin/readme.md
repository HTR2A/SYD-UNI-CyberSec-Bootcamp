# A Day in the Life of a Windows Sysadmin

## Task 1: Create a GPO—Disable Local Link Multicast Name Resolution (LLMNR)

### Scenario
In this task, you investigated LLMNR vulnerabilities and mitigated the risks by disabling LLMNR on Windows 10 machines within the GC Computers Organizational Unit (OU).

**LLMNR** is a protocol used by Windows as a backup for DNS to locate network resources. The vulnerability arises because LLMNR accepts any response, making it susceptible to spoofing attacks. By disabling LLMNR, you prevent attackers from injecting false responses into your network.

### Steps Taken
1. **Open Group Policy Management Tool**: In the Windows Server environment, open the Group Policy Management tool from the Server Manager.
2. **Create a New GPO**: Right-click **Group Policy Objects** and select **New**. Name the GPO as **No LLMNR**.
3. **Edit GPO**:
   - Right-click **No LLMNR** and select **Edit**.
   - Navigate to **Computer Configuration > Policies > Administrative Templates > Network > DNS Client**.
   - Enable the policy named **Turn Off Multicast Name Resolution**.
4. **Link GPO to GC Computers OU**: Link the **No LLMNR** GPO to the **GC Computers** OU.
![Step 1](https://github.com/user-attachments/assets/a52d4491-5f85-4629-9974-003f484e3fe7)

---

## Task 2: Create a GPO—Account Lockout Policy

### Scenario
To prevent brute-force attacks on Windows workstations, an account lockout policy was created. This policy limits the number of failed login attempts before an account is locked, reducing the risk of unauthorized access.

### Steps Taken
1. **Create a New GPO**: Named the GPO as **Account Lockout**.
2. **Edit GPO**:
   - Navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy**.
   - Set the following:
     - **Account lockout duration**: 15 minutes.
     - **Account lockout threshold**: 10 invalid login attempts.
     - **Reset account lockout counter after**: 15 minutes.
3. **Link GPO to GC Computers OU**: Link the **Account Lockout** GPO to the **GC Computers** OU.

---

## Task 3: Create a GPO—Enabling Verbose PowerShell Logging and Transcription

### Scenario
PowerShell is a common tool for attackers. To enhance visibility and improve monitoring, verbose PowerShell logging and transcription were enabled via a new GPO.

### Steps Taken
1. **Create a New GPO**: Named the GPO **PowerShell Logging**.
2. **Edit GPO**:
   - Navigate to **Computer Configuration > Policies > Administrative Templates > Windows Components > Windows PowerShell**.
   - Enable the following policies:
     - **Turn on Module Logging**: Log all PowerShell modules.
     - **Turn on PowerShell Script Block Logging**: Logs script blocks for better monitoring.
     - **Turn on PowerShell Transcription**: Enabled, with the **Include invocation headers** option checked.
3. **Link GPO to GC Computers OU**: Link the **PowerShell Logging** GPO to the **GC Computers** OU.

---

## Task 4: Create a Script—Enumerate Access Control Lists (ACLs)

### Scenario
This task involved creating a PowerShell script that enumerates ACLs for each file or subdirectory within the current directory. This is useful for reviewing permissions and identifying potential misconfigurations.

### PowerShell Script (`enum_acls.ps1`)
```powershell
# Define the directory variable
$directory = Get-ChildItem

# Loop through each item in the directory
foreach ($item in $directory) {
    # Enumerate the ACL for each item
    Get-Acl $item.FullName
}
```
- **Script Location**: The script was saved at `C:\Users\sysadmin\Documents\enum_acls.ps1`.
- **Execution Example**:
  - Open a PowerShell window.
  - Move to a directory (e.g., `cd C:\Windows`).
  - Run the script with: `C:\Users\sysadmin\Documents\enum_acls.ps1`.

### Script Output
The script output showed the ACL details for each file and directory, allowing visibility into user permissions. This can help identify over-permissioned users or security risks.

---

## Task 5: Verify PowerShell Logging GPO

### Scenario
After configuring the PowerShell logging GPO, the next step was to verify if the logging was working correctly.

### Steps Taken
1. **Run `gpupdate`**: In an administrative PowerShell session, run `gpupdate /force` to pull the latest policy changes.
2. **Run the Script**:
   - Navigate to a directory such as `C:\Windows`.
   - Run the `enum_acls.ps1` script.
3. **Check Logs**:
   - Navigate to `C:\Users\sysadmin\Documents`.
   - Locate the transcription logs, stored in a folder with the current date.

**Issues Encountered**:
- The `gpupdate` command displayed errors related to **Name Resolution Failure** and **Active Directory Replication Latency**. These may be related to domain replication issues or network configuration problems.

---

This completes the day-to-day tasks, providing an overview of Group Policy creation and verification processes, as well as PowerShell scripting to ensure security and compliance. Let me know if you need any additional edits or further details on any specific tasks!


