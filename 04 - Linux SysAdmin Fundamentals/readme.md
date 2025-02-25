# Linux SysAdmin Fundamentals

---

### Step 1: Ensure Permissions on Sensitive Files
In this step, we verified and updated permissions for important system files to ensure security. The commands and required permissions were as follows:

- **Navigate to /etc directory**:
  ```
  cd /etc/
  ```
- **View File Permissions**: Used the following command to view the current file permissions for each file:
  ```
  ls -l <file>
  ```
- **Set Correct Permissions**:
  - Set permissions on `/etc/shadow` to allow only root read and write access:
    ```
    sudo chmod 600 /etc/shadow
    ```
  - **Explanation**: The octal notation `600` ensures only root has read and write access.
  - Set permissions on `/etc/gshadow` to allow only root read and write access:
    ```
    sudo chmod 600 /etc/gshadow
    ```
  - Set permissions on `/etc/group` to allow root read and write access, and allow everyone else read access only:
    ```
    sudo chmod 644 /etc/group
    ```
  - **Explanation**: The octal notation `644` allows root to read and write, and everyone else to read only.
  - Set permissions on `/etc/passwd` to allow root read and write access, and allow everyone else read access only:
    ```
    sudo chmod 644 /etc/passwd
    ```

### Step 2: Create User Accounts
This step involved adding user accounts to the system using the `useradd` command:

- **Add Users**:
  - Add user `sam`:
    ```
    sudo useradd sam
    ```
  - Add user `joe`:
    ```
    sudo useradd joe
    ```
  - Add user `amy`:
    ```
    sudo useradd amy
    ```
  - Add user `sara`:
    ```
    sudo useradd sara
    ```
  - Add user `admin1`:
    ```
    sudo useradd admin1
    ```

- **Add Admin1 to Sudo Group**:
  - Give `admin1` sudo privileges:
    ```
    sudo usermod -aG sudo admin1
    ```

### Step 3: Create User Group and Collaborative Folder
The next step involved setting up a group for collaboration and creating a shared folder:

- **Create the Engineers Group**:
  ```
  sudo groupadd engineers
  ```

- **Add Users to the Engineers Group**:
  - Add `sam` to the engineers group:
    ```
    sudo usermod -aG engineers sam
    ```
  - **Explanation**: The `-aG` flag is used to add a user to a group without removing them from other groups.
  - Repeat the above command to add `joe`, `amy`, and `sara` to the engineers group.

- **Create Shared Folder**:
  - Create a shared folder for the engineers group:
    ```
    sudo mkdir /home/engineers
    ```

- **Change Ownership of the Shared Folder**:
  - Change the ownership of `/home/engineers` to the engineers group:
    ```
    sudo chown :engineers /home/engineers
    ```

### Step 4: Lynis Auditing
The final step was to run a security audit using Lynis to identify areas of improvement for hardening the system:

- **Install Lynis**:
  - If Lynis was not installed, used the following command to install it:
    ```
    sudo apt-get install lynis
    ```

- **Run Lynis System Audit**:
  ```
  sudo lynis audit system
  ```

- **Audit Results**: Reviewed the Lynis report and documented recommendations for system hardening, including suggestions for improving file permissions, disabling unnecessary services, and enforcing stronger password policies.

---

## Summary of Findings and Recommendations
The server setup process ensured proper permissions on sensitive files, added user accounts, configured group permissions, and created a collaborative workspace for the engineers group. The Lynis audit identified areas of improvement for system hardening, which included:

- **File Permissions**: Ensure critical files are only accessible by authorized users.
- **Password Policies**: Enforce stronger password policies to enhance security.
- **Service Management**: Disable unnecessary services to reduce the attack surface.

These steps will ensure a more secure and properly configured server ready to replace the malfunctioning one.

