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
<img width="1252" alt="CreateVM-b" src="https://github.com/user-attachments/assets/24b52a09-1dae-4b27-8ae2-eadec368c8d3">



- **Web VMs (VM2 and VM3)**: I also deployed two additional VMs named "Web-1" and "Web-2," both linked to the same resource group and VNet as the Jump Box.
  - These web VMs were configured without public IPs, ensuring that they are only accessible from within the network.

<img width="806" alt="WebVMNetworking" src="https://github.com/user-attachments/assets/3da6aba7-769b-4cda-b736-2d1f995d5ee0">


### 5. Adding Security Group Rules for the Jump Box

To ensure secure management of the cloud environment, I added a rule to the Network Security Group to allow SSH access from my current IP address.

- **Inbound Security Rule**: Configured to allow SSH traffic from my IP address only, using port 22 and TCP protocol.

*Insert Image Here*: **Screenshot of the inbound security rule for SSH access, highlighting the source as "My IP" and the destination port as 22.**

<img width="293" alt="limit-ip-ssh" src="https://github.com/user-attachments/assets/24f2ae14-3c2e-41a1-bfd7-f67f3eb3dd14">

### 6 Detailed Docker Container Setup

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
- **Check Docker Service**: To confirm Docker was installed and running properly, I used:
  ```
  sudo systemctl status docker
  ```
  - If the service was not running, I started it with:
    ```
    sudo systemctl start docker
    ```

<img width="972" alt="Docker_Install" src="https://github.com/user-attachments/assets/5bf576fe-f90f-44be-91ec-3e95057c9d89">



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
<img width="209" alt="JumpBox_settings1" src="https://github.com/user-attachments/assets/09457d2c-7c7f-4784-b575-229d31728114">




## **Provisioners**

1. **Launch a New VM in Azure Portal**:

   - Access the Azure portal and launch a new Virtual Machine (VM).
   - Configure the VM to only allow SSH access using a new SSH key generated from a container running in your jump box.

2. **Connect to Ansible Container**:

   - From your jump box, connect to the Ansible container.
   - Run the following command to list Docker containers and find your Ansible container:
     ```
     sudo docker container list -a
     ```
   - Use the command below to start and connect to your Ansible container:
     ```
     docker run -it cyberxsecurity/ansible /bin/bash
     ```
   - Your prompt should change to reflect the container’s shell environment.

3. **Generate a New SSH Key**:

   - Once inside the Ansible container, run the following command to create a new SSH key:
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

   - Accept the default location for saving the key (`/root/.ssh/id_rsa`) and leave the passphrase empty.

   - Verify that the key pair was created by listing the files in the `.ssh` directory:

     ```
     ls .ssh/
     ```

   - Display the public key to copy it:

     ```
     cat .ssh/id_rsa.pub
     ```

   ```
   root@23b86e1d62ad:~# cat .ssh/id_rsa.pub
   ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDz5KX3urPPKbYRKS3J06wyw5Xj4eZRQTcg6u2LpnSsXwPWYBpCdF5lE3tJlbp7AsnXlXpq2G0oAy5dcLJX2anpfaEBTEvZ0mFBS24AdNnF3ptan5SmEM/

   ```

4. **Update Azure VM with the New SSH Key**:

   - Go back to the Azure portal.
   - Locate your newly created Web VM's details page.
   - Reset the SSH public key for the VM by pasting in the public key generated from the Ansible container.

5. **Retrieve Internal IP Address**:

   - From the Azure portal, get the internal IP address of your VM.

![reset-ssh](https://github.com/user-attachments/assets/15a66cc0-c63f-4707-aa90-396073456804)


6. **Test SSH Connection to the VM**:

   - In your Ansible container, attempt to connect to the VM using the internal IP address:
     ```
     ssh ansible@<internal-ip>
     ```
   - Accept the authenticity of the host by typing "yes" when prompted.
   - The connection was successful, we see a welcome message from the Ubuntu system.

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



- To exit the SSH session, run:
  ```
  exit
  ```
7. **Update Ansible Hosts File**:
  - Locate the Ansible hosts file in the container:
    ```
    ls /etc/ansible/
    ```
  - Open the hosts file with `nano` to edit:
    ```
    nano /etc/ansible/hosts
    ```
  - Uncomment the `[webservers]` header.
  - Add the internal IP address of your VM under the `[webservers]` header along with the Python interpreter line:
    ```
    10.0.0.6 ansible_python_interpreter=/usr/bin/python3
    ```

Output

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

8. **Update Ansible Configuration File**:

   - Open the Ansible configuration file to specify the default SSH user:
     ```
     nano /etc/ansible/ansible.cfg
     ```
   - Scroll to the `remote_user` option, uncomment it, and set it to your administrator username:
     ```
     remote_user = sysadmin
     ```

9. **Test Ansible Connection**:

   - Run the following Ansible command to test the connection to your configured hosts:
     ```
     ansible all -m ping
     ```
   - If configured correctly, you should see output indicating a successful connection, similar to:
     ```
     10.0.0.6 | SUCCESS => {
       "changed": false,
       "ping": "pong"
     }
     ```










