# Module 13 - Cloud Environment Setup

## Overview

This document details the setup of my cloud network environment, focusing on creating a virtual network, configuring security groups, and launching virtual machines. I'll describe each step I followed.

### 1. Setting Up the Resource Group

The first step was to create a resource group using the Azure portal. This resource group is essentially the container that holds all the cloud resources needed for the project. I used the following procedure:

- **Search for "resource"** in the Azure portal home screen.
- Click on the **"+ Add"** or **"Create resource group"** button.
- Choose a name for the resource group, ensuring it’s easily identifiable, and select a specific region.

![Create resource group](https://github.com/user-attachments/assets/5c5095a5-0fac-48ae-ba27-f261383b985f)


### 2. Creating the Virtual Network (VNet)
![Create virtual network_1](https://github.com/user-attachments/assets/ecd13b65-4704-4d04-876a-ca447ba4c83e)


With the resource group in place, I set up the Virtual Network (VNet). The VNet serves as the foundation for deploying virtual machines and other services.

- **Navigate to "Virtual networks"** by searching "net" in the Azure portal.
- Click on the **"+ Add"** button to create a new virtual network.
- I filled in the network settings, including selecting the resource group I created earlier, naming the VNet, and specifying the same region as the resource group.
- Used default settings for **IP addresses** and **Security**, but ensured that **DDoS Protection Standard** was disabled to avoid unnecessary costs.

<img width="793" alt="vNet1" src="https://github.com/user-attachments/assets/5fc4da67-023a-4251-b86b-918127ae2f82">
<img width="773" alt="vNet2" src="https://github.com/user-attachments/assets/08ce309f-e603-4577-bfe8-7ed27c9f6468">
<img width="856" alt="vNet3" src="https://github.com/user-attachments/assets/fca4d5f9-f80f-4b60-af0b-d3c1d3e0e8e6">
<img width="774" alt="vNet4" src="https://github.com/user-attachments/assets/b15767db-8977-4032-9d0d-63be861ae593">
<img width="531" alt="vNet5" src="https://github.com/user-attachments/assets/aff8aff3-68e9-42e9-9728-e51cea1d274b">


### 3. Configuring the Network Security Group (NSG)

The Network Security Group (NSG) was set up to manage the flow of network traffic, enhancing the security of the environment.

- **Search for "Network security groups"** in Azure.
- Add the NSG to my resource group and provide it with a recognizable name.
- Configured **inbound security rules** to block all traffic initially, then added specific rules for allowing certain types of traffic, such as SSH.

![inbound_rules](https://github.com/user-attachments/assets/dff73cb6-4513-47a4-93b5-122aff7d6c8b)
![inbound_rules_2](https://github.com/user-attachments/assets/959525c6-0226-4beb-ac72-d740ef4ab8cd)


### 4. Launching the Virtual Machines

Next, I created the virtual machines (VMs) that are essential for the project:

- **Jump Box (VM1)**: This is the first virtual machine, known as the "JumpBoxProvisioner," which I used to access other machines securely.
  - **Virtual network**: Selected the previously created VNet.
  - **Security group**: Linked to the NSG to apply security policies.
  - **SSH Authentication**: Generated an SSH key and used it for secure access.
```
m3air@Jasons-Air ~ % ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/cyber/.ssh/id_rsa):
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in id_rsa.
Your public key has been saved in id_rsa.pub.
The key fingerprint is:
SHA256:r3aBFU50/5iQbbzhqXY+fOIfivRFdMFt37AvLJifC/0 cyber@2Us-MacBook-Pro.local
The randomart image is:
+---[RSA 2048]----+
|         .. . ...|
|          o. =..+|
|         o .o *=+|
|          o  +oB+|
|        So o .*o.|
|        ..+...+ .|
|          o+++.+ |
|        ..oo=+* o|
|       ... ..=E=.|
+----[SHA256]-----+
```

```
cat ~/.ssh/id_rsa.pub
```

```
m3air@Jasons-Air ~ % cat ~/.ssh/id_rsa.pub 

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDGG6dBJ6ibhgM09U+kn/5NE7cGc4CNHWXein0f+MciKElDalf76nVgFvJQEIImMhAGrtRRJDAd6itlPyBpurSyNOByU6LX7Gl6DfGQKzQns6+n9BheiVLLY9dtodp8oAXdVEGles5EslflPrTrjijVZa9lxGe34DtrjijExWM6hBb0KvwlkU4worPblINx+ghDv+3pdrkUXMsQAht/fLdtP/EBwgSXKYCu/

```

<img width="816" alt="Jump_box-VM" src="https://github.com/user-attachments/assets/595ffb43-8e90-4ac2-b186-1d7f23a4366a">



- **Web VMs (VM2 and VM3)**: I also deployed two additional VMs named "Web-1" and "Web-2," both linked to the same resource group and VNet as the Jump Box.

<img width="1208" alt="Web-1-AvailabilitySet" src="https://github.com/user-attachments/assets/d59122f5-d6b9-4bcc-a6c4-e39d3e5d730e">


- These web VMs were configured without public IPs, ensuring that they are only accessible from within the network.

<img width="806" alt="WebVMNetworking" src="https://github.com/user-attachments/assets/3da6aba7-769b-4cda-b736-2d1f995d5ee0">


## 5. Jump Box Administration

The goal of this activity was to create a security group rule to allow SSH connections only from my current IP address and to connect to the new virtual machine for management.

### 1. Find My IP Address

- First, I found my IP address by opening the terminal and entering the command:
  ```
  curl icanhazip.com
  ```
  - Alternatively, I could google "What's my IP address?"

### 2. Log into Azure Portal

- I logged into `portal.azure.com` to create a security group rule that allows SSH connections from my current IP address.

### 3. Create a Security Group Rule

- I found my security group listed under my resource group.
- I created a rule allowing SSH connections from my IP address by following these steps:
  - On the left, I selected **Inbound security rules**.
  - I clicked **+ Add** to add a rule.
  - I configured the rule as follows:
    - **Source**: Set to "My IP address".
      - Note: I verified that the IP address shown matched the address from step 1.
    - **Source Port Ranges**: Set to "Any".
    - **Destination**: Set to "Service Tag/Virtual Network", but a better setting was to specify the internal IP of my jump box to really limit this traffic.
    - **Service**: Set to "SSH".
    - **Destination Port Ranges**: Defaulted to port 22 as I selected SSH for the service.
    - **Protocol**: Defaulted to TCP.
    - **Action**: Set to "Allow".
    - **Priority**: Set to a lower number than my rule to deny all traffic (i.e., less than 4,096).
    - **Name**: Named the rule appropriately, such as "SSH".
    - **Description**: Wrote a short description like "Allow SSH from my IP".
   
<img width="293" alt="limit-ip-ssh" src="https://github.com/user-attachments/assets/24f2ae14-3c2e-41a1-bfd7-f67f3eb3dd14">

### 4. SSH to the VM for Administration

- I used my command line to SSH to the VM for administration. Windows users should use GitBash.
- The command to connect was:
  ```
  ssh admin-username@VM-public-IP
  ```
  - I used the username I had previously set up. My SSH key was used automatically.
- The first time I connected, I needed to type "yes" to add the machine to my list of known hosts.

### 5. Check Sudo Permissions

- Once connected, I checked my sudo permissions by running the command:
  ```
  sudo -l
  ```
  - I noticed that my admin user had full sudo permissions without requiring a password.

### Note

Please note that my public IP address will change depending on my location.
- In a normal work environment, I would set up a static IP address to avoid continually creating rules to allow access to my cloud machine.
- In my case, I would need to create another security rule to allow my home network to access my Azure VM.

**Note**: If I needed to reset my SSH key, I could do so on the VM details page by selecting **Reset Password** on the left-hand column.

![password-reset](https://github.com/user-attachments/assets/0f09e0b4-22a5-44eb-93d8-d838d912f126)


### 6. Docker Container Setup

After initial configuration, I proceeded with setting up Docker on the Jump Box to manage containers effectively. Here is how I did it:

- **SSH into the Jump Box**: First, I opened my terminal and used SSH to connect to the Jump Box:
  ```
  ssh admin@jump-box-ip
  ```
- **Update Machine**: Once connected, I ran the following command to update the Jump Box:
  ```
  sudo apt-get update
  ```
- **Install Docker**: Next, I installed Docker using the command:
  ```
  sudo apt install docker.io
  ```

<img width="972" alt="Docker_Install" src="https://github.com/user-attachments/assets/5bf576fe-f90f-44be-91ec-3e95057c9d89">

- **Check Docker Service**: To confirm Docker was installed and running properly, I used:
  ```
  sudo systemctl status docker
  ```
- If the service was not running, I started it with:
  ```
  sudo systemctl start docker
  ```


- **Pull Docker Image**: With Docker running, I pulled the required container image:
  ```
  sudo docker pull cyberxsecurity/ansible
  ```
  - This command downloaded the "cyberxsecurity/ansible" container from Docker Hub.

<img width="1392" alt="Docker_Process" src="https://github.com/user-attachments/assets/b2cbfdff-e4be-4c74-89c1-da23496dcd94">
<img width="857" alt="Docker_Pull" src="https://github.com/user-attachments/assets/ffc52ba4-10da-44e1-a076-a3c30f82c133">


- **Run the Docker Container**: Finally, I launched the Ansible container interactively:
  ```
  sudo docker run -ti cyberxsecurity/ansible bash
  ```
  - The `-ti` flag allowed me to open an interactive terminal to work inside the container.

<img width="1162" alt="Container_Connected" src="https://github.com/user-attachments/assets/fe36363b-2b5a-4a3a-874a-1ff80f6b98ca">



- **Setting Up Security Group Rules**: To allow the Jump Box to interact with the virtual network securely, I configured the Network Security Group (NSG) to enable SSH access from the Jump Box to other resources in the VNet:
  - **Source**: IP Addresses setting with the internal IP of the Jump Box.
  - **Source port ranges**: Set to `*`.
  - **Destination**: Set to VirtualNetwork.
  - **Service**: Select SSH.
  - **Destination port ranges**: Port `22`.
  - **Action**: Allow traffic.
  - **Priority**: Set to a lower number to ensure the rule has precedence.


<img width="1349" alt="VM_IP_Address" src="https://github.com/user-attachments/assets/7e894409-b4f1-41ed-b6de-3572814e6783">
<img width="350" alt="JumpBox_settings1" src="https://github.com/user-attachments/assets/09457d2c-7c7f-4784-b575-229d31728114">

## 7. Provisioner Setup

### 1. Launch a New VM in Azure Portal

- I accessed the Azure portal and launched a new Virtual Machine (VM).
- I configured the VM to only allow SSH access using a new SSH key generated from a container running in my jump box.

### 2. Connect to Ansible Container

- From my jump box, I connected to the Ansible container.
- I ran the following command to list Docker containers and locate my Ansible container:
  ```
  sudo docker container list -a
  ```
- I used the command below to start and connect to the Ansible container:
  ```
  docker run -it cyberxsecurity/ansible /bin/bash
  ```
- My prompt changed to reflect the container’s shell environment.

### 3. Generate a New SSH Key

- Once inside the Ansible container, I created a new SSH key using the following command:
  ```
  ssh-keygen -t rsa
  ```
  ```
  ~root@23b86e1d62ad:~# ssh-keygen -t rsa

  Generating public/private rsa key pair.

  Enter file in which to save the key (/root/.ssh/id_rsa):

  Created directory '/root/.ssh'.

  Enter passphrase (empty for no passphrase):

  Enter same passphrase again:

  Your identification has been saved in /root/.ssh/id_rsa.

  Your public key has been saved in /root/.ssh/id_rsa.pub.

  The key fingerprint is:

  SHA256:gzoKliTqbxvTFhrNU7ZwUHEx7xAA7MBPS2Wq3HdJ6rw root@23b86e1d62ad

  The key's randomart image is:

  +---[RSA 2048]----+
  |  . .o+*o=.      |
  |   o ++ . +      |
  |    *o.+ o .     |
  |  . =+=.+ +      |
  |.. + *.+So .     |
  |+ . +.* ..       |
  |oo +oo o         |
  |o. o+.  .        |
  | .+o.  E         |
  +----[SHA256]-----+
  root@23b86e1d62ad:~#
  ```
- I accepted the default location for saving the key (`/root/.ssh/id_rsa`) and left the passphrase empty.
- I verified that the key pair was created by listing the files in the `.ssh` directory:
  ```
  ls .ssh/
  ```
- I displayed the public key to copy it:
  ```
  cat .ssh/id_rsa.pub
  ```
  ```
  root@23b86e1d62ad:~# cat .ssh/id_rsa.pub
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDz5KX3urPPKbYRKS3J06wyw5Xj4eZRQTcg6u2LpnSsXwPWYBpCdF5lE3tJlbp7AsnXlXpq2G0oAy5dcLJX2anpfaEBTEvZ0mFBS24AdNnF3ptan5SmEM/
  ```

### 4. Update Azure VM with the New SSH Key

- I went back to the Azure portal.
- I located the newly created Web VM's details page.
- I reset the SSH public key for the VM by pasting in the public key generated from the Ansible container.

![reset-ssh](https://github.com/user-attachments/assets/15a66cc0-c63f-4707-aa90-396073456804)

### 5. Retrieve Internal IP Address

- From the Azure portal, I retrieved the internal IP address of my VM.


### 6. Test SSH Connection to the VM

- In the Ansible container, I attempted to connect to the VM using the internal IP address:
  ```
  ssh ansible@10.0.0.6
  ```
- I accepted the authenticity of the host by typing "yes" when prompted.
- The connection was successful, and I saw a welcome message from the Ubuntu system.
  ```
  root@23b86e1d62ad:~# ping 10.0.0.6
  PING 10.0.0.6 (10.0.0.6) 56(84) bytes of data.
  ^C
  --- 10.0.0.6 ping statistics ---
  4 packets transmitted, 0 received, 100% packet loss, time 3062ms

  root@23b86e1d62ad:~#
  ```
  ```
  root@23b86e1d62ad:~# ssh ansible@10.0.0.6
  The authenticity of host '10.0.0.6 (10.0.0.6)' can't be established.
  ECDSA key fingerprint is SHA256:7Wd1cStyhq5HihBf+7TQgjIQe2uHP6arx2qZ1YrPAP4.
  Are you sure you want to continue connecting (yes/no)? yes
  Warning: Permanently added '10.0.0.6' (ECDSA) to the list of known hosts.
  Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 5.0.0-1027-azure x86_64)

  * Documentation:  https://help.ubuntu.com
  * Management:     https://landscape.canonical.com
  * Support:        https://ubuntu.com/advantage

  System information as of Mon Jan  6 18:49:56 UTC 2020

  System load:  0.01              Processes:           108
  Usage of /:   4.1% of 28.90GB   Users logged in:     0
  Memory usage: 36%               IP address for eth0: 10.0.0.6
  Swap usage:   0%

  0 packages can be updated.
  0 updates are security updates.

  Last login: Mon Jan  6 18:33:30 2020 from 10.0.0.4
  To run a command as administrator (user "root"), use "sudo <command>".
  See "man sudo_root" for details.

  ansible@Pentest-1:~$
  ```
- To exit the SSH session, I ran:
  ```
  exit
  ```

### 7. Update Ansible Hosts File

- I located the Ansible hosts file in the container:
  ```
  ls /etc/ansible/
  ```
- I opened the hosts file with `nano` to edit:
  ```
  nano /etc/ansible/hosts
  ```
- I uncommented the `[webservers]` header.
- I added the internal IP address of my VM under the `[webservers]` header along with the Python interpreter line:
  ```
  10.0.0.6 ansible_python_interpreter=/usr/bin/python3
  ```
  ```
  # This is the default ansible 'hosts' file.
  #
  # It should live in /etc/ansible/hosts
  #
  #   - Comments begin with the '#' character
  #   - Blank lines are ignored
  #   - Groups of hosts are delimited by [header] elements
  #   - You can enter hostnames or ip addresses
  #   - A hostname/ip can be a member of multiple groups
  # Ex 1: Ungrouped hosts, specify before any group headers.

  ## green.example.com
  ## blue.example.com
  ## 192.168.100.1
  ## 192.168.100.10

  # Ex 2: A collection of hosts belonging to the 'webservers' group

  [webservers]
  ## alpha.example.org
  ## beta.example.org
  ## 192.168.1.100
  ## 192.168.1.110
  10.0.0.6 ansible_python_interpreter=/usr/bin/python3
  10.0.0.7 ansible_python_interpreter=/usr/bin/python3
  ```

### 8. Update Ansible Configuration File

- I opened the Ansible configuration file to specify the default SSH user:
  ```
  nano /etc/ansible/ansible.cfg
  ```
- I scrolled to the `remote_user` option, uncommented it, and set it to my administrator username "sysadmin":
  
  ```
  # What flags to pass to sudo
  # WARNING: leaving out the defaults might create unexpected behaviours
  #sudo_flags = -H -S -n

  # SSH timeout
  #timeout = 10

  # default user to use for playbooks if user is not specified
  # (/usr/bin/ansible will use current user as default)
  remote_user = sysadmin

  # logging is off by default unless this path is defined
  # if so defined, consider logrotate
  #log_path = /var/log/ansible.log

  # default module name for /usr/bin/ansible
  #module_name = command
  ```

### 9. Test Ansible Connection

- I ran the following Ansible command to test the connection to my configured hosts:
  ```
  ansible all -m ping
  ```
- I saw output indicating a successful connection:

  ```
  10.0.0.5 | SUCCESS => {
  "changed": false, 
  "ping": "pong"
  }
  10.0.0.6 | SUCCESS => {
		"changed": false, 
		"ping": "pong"
  }
  ```


## 8. Ansible Playbooks

My task was to create an Ansible playbook that installed Docker and configured a VM with the DVWA web app.

### 1. Connect to Ansible Container

- I connected to my jump box and then to the Ansible container.
- If I had stopped or exited the container, I found it again using:
  ```
  docker container list -a
  ```
  ```
  root@Red-Team-Web-VM-1:/home/RedAdmin# docker container list -a
  CONTAINER ID        IMAGE                           COMMAND                  CREATED             STATUS                         PORTS               NAMES
  Exited (0) 2 minutes ago                           hardcore_brown
  a0d78be636f7        cyberxsecurity/ansible:latest   "bash"                   3 days ago  
  ```
- I started the container again using:
  ```
  docker start hardcore_brown
  ```
  ```
  root@Red-Team-Web-VM-1:/home/RedAdmin# docker start hardcore_brown
  hardcore_brown
  ```
- I got a shell in my container using:
  ```
  docker attach hardcore_brown
  ```
  ```
  root@Red-Team-Web-VM-1:/home/RedAdmin# docker attach hardcore_brown
  root@1f08425a2967:~#
  ```

### 2. Create a YAML Playbook File

- I created a YAML playbook file for the configuration:
  ```
  nano /etc/ansible/pentest.yml
  ```
- The top of my YAML file read:
  ```
  ---
  - name: Config Web VM with Docker
    hosts: webservers
    become: true
    tasks:
  ```

### 3. Uninstall Apache

- DVWA runs on port 80, so I needed to remove Apache if it was installed:
  ```
  - name: Uninstall apache if needed
    ansible.builtin.apt:
      update_cache: yes
      name: apache2
      state: absent
  ```

### 4. Install Docker and Python3-pip

- I used the Ansible `builtin.apt` module to install Docker and Python3-pip:
  ```
  - name: docker.io
    ansible.builtin.apt:
      update_cache: yes
      name: docker.io
      state: present

  - name: Install pip3
    ansible.builtin.apt:
      force_apt_get: yes
      name: python3-pip
      state: present
  ```

### 5. Install Python Docker Module

- I used the Ansible `pip` module to install Docker:
  ```
  - name: Install Python Docker module
    pip:
      name: docker
      state: present
  ```

### 6. Install DVWA Docker Container

- I used the Ansible `docker_container` module to install the DVWA container, ensuring port 80 was published:
  ```
  - name: download and launch a docker web container
    docker_container:
      name: dvwa
      image: cyberxsecurity/dvwa
      state: started
      restart_policy: always
      published_ports: 80:80
  ```

### 7. Enable Docker Service

- I used the `systemd` module to ensure Docker starts when the machine reboots:
  ```
  - name: Enable docker service
    systemd:
      name: docker
      enabled: yes
  ```

### 8. Run Ansible Playbook

- My final playbook looked like this:

  ```
  ---
  - name: Config Web VM with Docker
    hosts: webservers
    become: true
    tasks:

      - name: Uninstall apache if needed
        ansible.builtin.apt:
          update_cache: yes
          name: apache2
          state: absent

      - name: docker.io
        ansible.builtin.apt:
          update_cache: yes
          name: docker.io
          state: present

      - name: Install pip3
        ansible.builtin.apt:
          force_apt_get: yes
          name: python3-pip
          state: present

      - name: Install Docker python module
        pip:
          name: docker
          state: present

      - name: download and launch a docker web container
        docker_container:
          name: dvwa
          image: cyberxsecurity/dvwa
          state: started
          published_ports: 80:80

      - name: Enable docker service
        systemd:
          name: docker
          enabled: yes
  ```

- I ran the playbook using:

  ```
  ansible-playbook /etc/ansible/pentest.yml
  ```

- The output was:

  ```
  PLAY [Config Web VM with Docker] ***************************************************************

  TASK [Gathering Facts] *************************************************************************
  ok: [10.0.0.6]

  TASK [Uninstall apache if needed] **************************************************************
  changed: [10.0.0.6]

  TASK [docker.io] *******************************************************************************
  [WARNING]: Updating cache and auto-installing missing dependency: python-apt

  changed: [10.0.0.6]

  TASK [Install pip3] *****************************************************************************
  changed: [10.0.0.6]

  TASK [Install Docker python module] ************************************************************
  changed: [10.0.0.6]

  TASK [download and launch a docker web container] **********************************************
  changed: [10.0.0.6]

  PLAY RECAP *************************************************************************************
  10.0.0.6                   : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
  ```

### 9. Test DVWA

- To test that DVWA was running on the new VM, I SSHed to the new VM from the Ansible container:
  ```
  ssh sysadmin@10.0.0.6
  ```
  ```
  Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 5.0.0-1027-azure x86_64)

  * Documentation:  https://help.ubuntu.com
  * Management:     https://landscape.canonical.com
  * Support:        https://ubuntu.com/advantage

  System information as of Mon Jan  6 20:01:03 UTC 2020

  System load:  0.01              Processes:              122
  Usage of /:   9.9% of 28.90GB   Users logged in:        0
  Memory usage: 58%               IP address for eth0:    10.0.0.6
  Swap usage:   0%                IP address for docker0: 172.17.0.1

  18 packages can be updated.
  0 updates are security updates.

  Last login: Mon Jan  6 19:33:51 2020 from 10.0.0.4
  ```
- I ran the following command to test the connection:
  ```
  curl localhost/setup.php
  ```
- If everything was working, I received some HTML from the DVWA container:
  ```
  <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">

  <html xmlns="http://www.w3.org/1999/xhtml">

    <head>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />

      <title>Setup :: Damn Vulnerable Web Application (DVWA) v1.10 *Development*</title>

      <link rel="stylesheet" type="text/css" href="dvwa/css/main.css" />

      <link rel="icon" type="\image/ico" href="favicon.ico" />

      <script type="text/javascript" src="dvwa/js/dvwaPage.js"></script>

    </head>
  ```

## 9. Load Balancer

My task was to install a load balancer in front of the VM to distribute the traffic among more than one VM.

<img width="1390" alt="LBSearch" src="https://github.com/user-attachments/assets/56028867-74da-48f0-b8be-aa08966c5585">

### 1. Create a Load Balancer

- I started by creating a new load balancer and assigning it a static IP address.
- From the homepage, I searched for "load balancer" and created a new load balancer in my red team resource group.
- I gave the load balancer a unique name.
  
![CreateLB](https://github.com/user-attachments/assets/d650d0e0-0282-41d0-b691-983c70d44367)


### 2. Add a Frontend IP Address

- I added a frontend IP address to the load balancer.
- I provided a unique name for the IP address. This name was used to create a URL that mapped to the load balancer's IP address.
- I created a new public IP address.
  
![AddIP](https://github.com/user-attachments/assets/e40be2d3-9972-44af-bb09-c3e92940ce72)


### 3. Add a Backend Pool

- I added a backend pool to the load balancer.
- I included my Web VMs in the backend pool.
  
![backendPool](https://github.com/user-attachments/assets/3881e149-4022-4a80-b9df-5a80ae5ab5a1)
![backendpool2](https://github.com/user-attachments/assets/97e6f2f8-9b5f-492a-8f24-c1cfc707ea27)


### 4. Configure Health Probes

- I did not add any inbound or outbound rules.
- I configured the Health Probe by navigating to the load balancer I had just created.
- On the left, I selected "Health Probes" and clicked "Add" to create a new health probe.
- I gave the health probe a unique name, set the protocol to TCP, and used port 80.
- I set the interval to 5 seconds.
  
![HealthProbeSelect](https://github.com/user-attachments/assets/395f5ac9-1160-4ae8-9de6-ca15e394ffd4)
![HealthProbeSettings](https://github.com/user-attachments/assets/d81b0bb3-4ae8-49be-a13f-b912e9341940)


## 10. Setting up NSG Rule for DVWA Webservers



### 1. Create a Load Balancing Rule

- I created a load balancing rule to forward port 80 from the load balancer to my Red Team VNet.
- I provided the following configuration:
  - **Name**: I gave the rule an appropriate name that I could recognize later.
  - **IP Version**: Set to IPv4.
  - **Frontend IP Address**: There was only one option, so I selected it.
  - **Protocol**: Set to TCP for standard website traffic.
  - **Port**: Set to 80.
  - **Backend Port**: Set to 80.
  - **Backend Pool and Health Probe**: I selected the backend pool and health probe that I had previously configured.
  - **Session Persistence**: Changed to Client IP and protocol to ensure that users maintain the same session during their interactions.
  - **Idle Timeout**: Left at the default value of 4 minutes.
  - **Floating IP**: Left disabled.
 
  ![LBR_rules](https://github.com/user-attachments/assets/a2cd6e8f-f6e9-443d-a520-bc54ab260d3c)


### 2. Create a New Security Group Rule

- I created a new security group rule to allow port 80 traffic from the internet to my internal VNet.
- I used the following settings:
  - **Source**: Changed to my external IPv4 address.
  - **Source Port Ranges**: Set to "Any" to allow any source port, as they are chosen at random by the source computer.
  - **Destination**: Set to "VirtualNetwork" to allow traffic to reach my Virtual Network.
  - **Destination Port Ranges**: Set to 80 to only allow port 80 traffic.
  - **Protocol**: Set to TCP.
  - **Action**: Set to "Allow" to allow the traffic.
  - **Name**: I chose an appropriate name that I could recognize later.
 

![IP_LB_Inbound](https://github.com/user-attachments/assets/1b584468-7d6a-42b2-80ef-b7485062b132)

  

### 3. Remove Default Deny All Rule

- I removed the security group rule that blocked all traffic on my VNet to allow traffic from my load balancer.
- By removing the default deny-all rule, I allowed traffic from the load balancer to reach my VMs.





### 4. Verify DVWA Access

- I verified that I could reach the DVWA app from my browser over the internet.
- I opened a web browser and entered the frontend IP address for my load balancer with `/setup.php` added to the IP address.
  - For example: `http://40.122.71.120/setup.php`
 
![IP_LB_Inbound](https://github.com/user-attachments/assets/a55bc6a8-f4f7-4c59-896a-c7519b03c36d)


### Note

With the stated configuration, I could only access these machines from the specified location. To access them from another location, I would need to update the security group rule.



