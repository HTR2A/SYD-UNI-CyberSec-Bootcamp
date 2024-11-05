## Module 5 Challenge
**Started:** 23 Jun at 10:27  

### Quiz Instructions
**Archiving and Logging Data**

This Challenge assignment is designed to solidify and demonstrate your knowledge of the following concepts and tools:

- Creating a tar archive that excludes a directory using the `--exclude=` command option.
- Managing backups using cronjobs.
- Writing Bash scripts to create system resource usage reports.
- Performing log filtering using `journalctl`.
- Managing log file sizes using `logrotate`.
- Creating an auditing system to check for policy and file violations using `auditd`.

### Scenario
For this assignment, you will play the role of a security analyst at Credico Inc., a financial institution that offers checking, savings, and investment banking services.

The company collects, processes, and maintains a large database of private financial information for both consumer and business accounts. The data is maintained on a local server.

The company must comply with the Federal Trade Commission's Gramm-Leach-Bliley Act (GLBA), which requires that financial institutions explain their information-sharing practices to their customers and protect sensitive data.

In an effort to mitigate network attacks and meet federal compliance, Credico Inc. developed an efficient log management program that performs:

- Log size management using `logrotate`.
- Log auditing with `auditd` to track events, record the events, detect abuse or unauthorized activity, and create custom reports.

These tools, in addition to archives, backups, scripting, and task automation, contribute to a fully comprehensive log management system.

You will expand and enhance this log management system by learning new tools, adding advanced features, and researching additional concepts.

### Lab Environment
To set up your lab environment with the necessary files, complete the following steps:

1. Log into your web lab machine.
2. Create a directory called **Projects** in your `/home/sysadmin/` directory.
3. Download the following file (you can either slack it to yourself or use the Firefox browser in your Ubuntu machine), and move it to your `~/Projects` directory before you get started:

   **TarDocs.tar**

### Instructions
In each of the following sections, you will use and build on your system administration tools and knowledge. Make sure to read the instructions carefully. As you complete each step, make sure to take notes as you will use it to answer the questions in this quiz.

**IMPORTANT:** Please review your answers carefully before submitting to ensure that they are free of spelling and spacing errors. Incorrect spelling or incorrect spacing syntax will be marked as incorrect answers.

### Step 1: Create, Extract, Compress, and Manage tar Backup Archives
Creating tar archives is something you must do every day in your role at Credico Inc. In this section, you will extract and exclude specific files and directories to help speed up your workflow.

- Navigate to the `~/Projects` directory, where your downloaded **TarDocs.tar** archive file should be.
- Extract the `TarDocs.tar` archive file into the current directory (`~/Projects`). Then, list the directory's contents with `ls` to verify that you have extracted the archive properly.
  - **Command:**
    ```
    tar xvvf TarDocs.tar
    ```
- Verify that there is a **Java** subdirectory in the `TarDocs/Documents` folder by running `ls -l ~/Projects/TarDocs/Documents/`.
- Create a tar archive called **Javaless_Docs.tar** that excludes the **Java** directory from the newly extracted `TarDocs/Document/` directory.
  - **Command:**
    ```
    tar cvvf Javaless_Docs.tar --exclude="TarDocs/Documents/Java" TarDocs/
    ```
- Verify that this new `Javaless_Docs.tar` archive does not contain the **Java** subdirectory by using `tar` to list the contents of `Javaless_Docs.tar` and then piping `grep` to search for "Java".
  - **Command:**
    ```
    tar -tvf Javaless_Docs.tar | grep Java
    ```

**Optional Additional Challenge**

Create an incremental archive called `logs_backup.tar.gz` that contains only changed files by examining the `snapshot.file` for the `/var/log` directory. You will need `sudo` for this command.

### Step 2: Create, Manage, and Automate Cronjobs
In response to a ransomware attack, you have been tasked with creating an archiving and backup scheme to mitigate against CryptoLocker malware. This attack would encrypt the entire server’s hard disk and can only be unlocked using a 256-bit digital key after a Bitcoin payment is delivered.

- **Archiving Cronjob:**
  - Create an archiving cronjob to run every Wednesday at 6 am to create an archive of `/var/log/auth.log` with the filename and location `/auth_backup.tgz`.
  - **Cronjob Line:**
    ```
    0 6 * * 4 tar -zcf /auth_backup.tgz /var/log/auth.log
    ```

### Step 3: Write Basic Bash Scripts
Portions of the Gramm-Leach-Bliley Act require organizations to maintain a regular backup regimen for the safe and secure storage of financial data.

- **Create Backup Directories Using Brace Expansion**:
  - **Command:**
    ```
    mkdir -p ~/backups/{freemem,diskuse,openlist,freedisk}
    ```
- **Create a Script (system.sh)**
  - **Prints Free Memory:**
    ```
    free -h > ~/backups/freemem/free_mem.txt
    ```
  - **Prints Disk Usage:**
    ```
    df -h > ~/backups/diskuse/disk_usage.txt
    ```
  - **Lists All Open Files:**
    ```
    lsof > ~/backups/openlist/open_list.txt
    ```
  - **Prints Disk Space Statistics:**
    ```
    df -h > ~/backups/freedisk/free_disk.txt
    ```
- **Make `system.sh` Executable:**
  - **Command:**
    ```
    chmod +x system.sh
    ```
- **Add to System-Wide Weekly Cron Directory**:
  - **Command:**
    ```
    sudo cp system.sh /etc/cron.weekly
    ```

### Step 4: Manage Log File Sizes
You’ve decided to implement log rotation in order to preserve log entries and keep log file sizes more manageable.

- **Configure `logrotate` for /var/log/auth.log**:
  - **Settings:**
    - Rotate weekly.
    - Retain the seven most recent logs.
    - No rotation for empty logs.
    - Delay compression.
    - Skip errors for missing logs.
  - **Add the configuration in `/etc/logrotate.conf` surrounded by `{}`.**

### Optional Additional Challenge: Check for Policy and File Violations
- **Verify `auditd` Service**:
  - **Command:**
    ```
    systemctl status auditd
    ```
- **Edit `/etc/audit/auditd.conf`**:
  - **Parameters**:
    - Number of retained logs is 7.
    - Maximum log file size is 35.
- **Edit `/etc/audit/rules.d/audit.rules`**:
  - Create rules to monitor:
    - `/etc/shadow` with `wra` permissions, keyname: `hashpass_audit`.
    - `/etc/passwd` with `wra` permissions, keyname: `userpass_audit`.
    - `/var/log/auth.log` with `wra` permissions, keyname: `authlog_audit`.
- **Restart `auditd` Daemon**:
  - **Command:**
    ```
    sudo systemctl restart auditd
    ```

### Optional Additional Challenge: Perform Various Log Filtering Techniques
- **Filter Logs Using `journalctl`**
  - **Retrieve All Messages from Emergency to Error**:
    ```
    sudo journalctl -p 0..3 -b
    ```
  - **Check Disk Usage of Journal**:
    ```
    sudo journalctl --disk-usage
    ```
  - **Remove All Archived Journal Files Except the Most Recent Two**:
    ```
    sudo journalctl --vacuum-files=2
    ```
  - **Filter Priority Levels 0-2 and Save to File**:
    ```
    sudo journalctl -p 0..2 > /home/student/Priority_High.txt
    ```

---
End of Module 5 Challenge.

