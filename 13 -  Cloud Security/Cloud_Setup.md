# Module 13 - Cloud Environment Setup

## Overview

This document details the setup of my cloud network environment, focusing on creating a virtual network, configuring security groups, and launching virtual machines. I'll describe each step I followed.

### 1. Setting Up the Resource Group

The first step was to create a resource group using the Azure portal. This resource group is essentially the container that holds all the cloud resources needed for the project. I used the following procedure:

- **Search for "resource"** in the Azure portal home screen.
- Click on the **"+ Add"** or **"Create resource group"** button.
- Choose a name for the resource group, ensuring it’s easily identifiable, and select a specific region.

![Create virtual network_2](https://github.com/user-attachments/assets/dc3fc93a-fd6b-4e24-805e-bfaea69a21d1)
![Create virtual network_1](https://github.com/user-attachments/assets/a1938c65-c2d4-405a-9092-34bd076c7cbf)

### 2. Creating the Virtual Network (VNet)

With the resource group in place, I set up the Virtual Network (VNet). The VNet serves as the foundation for deploying virtual machines and other services.

- **Navigate to "Virtual networks"** by searching "net" in the Azure portal.
- Click on the **"+ Add"** button to create a new virtual network.
- I filled in the network settings, including selecting the resource group I created earlier, naming the VNet, and specifying the same region as the resource group.
- Used default settings for **IP addresses** and **Security**, but ensured that **DDoS Protection Standard** was disabled to avoid unnecessary costs.

<img width="793" alt="vNet1" src="https://github.com/user-attachments/assets/efc49a2e-5622-4ef3-9b35-87f36186866c">
<img width="773" alt="vNet2" src="https://github.com/user-attachments/assets/b1dcfa6a-4160-4c8b-9b58-1c8e1962616b">
<img width="856" alt="vNet3" src="https://github.com/user-attachments/assets/47b686ef-4224-4421-a659-954c2207529e">
<img width="774" alt="vNet4" src="https://github.com/user-attachments/assets/d1cf08fa-ae7b-40be-8ede-b8b27d09402e">
<img width="531" alt="vNet5" src="https://github.com/user-attachments/assets/17211f65-2029-476b-99a2-43869334debb">



### 3. Configuring the Network Security Group (NSG)

The Network Security Group (NSG) was set up to manage the flow of network traffic, enhancing the security of the environment.

- **Search for "Network security groups"** in Azure.
- Add the NSG to my resource group and provide it with a recognizable name.
- Configured **inbound security rules** to block all traffic initially, then added specific rules for allowing certain types of traffic, such as SSH.

*Insert Image Here*: **Screenshot of the Network Security Group with inbound rules settings, highlighting the "Default-Deny" rule.**

### 4. Launching the Virtual Machines

Next, I created the virtual machines (VMs) that are essential for the project:

- **Jump Box (VM1)**: This is the first virtual machine, known as the "JumpBoxProvisioner," which I used to access other machines securely.
  - **Virtual network**: Selected the previously created VNet.
  - **Security group**: Linked to the NSG to apply security policies.
  - **SSH Authentication**: Generated an SSH key and used it for secure access.

*Insert Image Here*: **Screenshot of the Jump Box creation screen, showing the SSH key setup and network settings.**

- **Web VMs (VM2 and VM3)**: I also deployed two additional VMs named "Web-1" and "Web-2," both linked to the same resource group and VNet as the Jump Box.
  - These web VMs were configured without public IPs, ensuring that they are only accessible from within the network.

*Insert Image Here*: **Screenshot of the Web VM networking tab, showing the subnet and the absence of a public IP address.**

### 5. Adding Security Group Rules for the Jump Box

To ensure secure management of the cloud environment, I added a rule to the Network Security Group to allow SSH access from my current IP address.

- **Inbound Security Rule**: Configured to allow SSH traffic from my IP address only, using port 22 and TCP protocol.

*Insert Image Here*: **Screenshot of the inbound security rule for SSH access, highlighting the source as "My IP" and the destination port as 22.**

### 6. Summary

This cloud environment setup involved configuring foundational cloud elements, including a resource group, virtual network, security group, and virtual machines. Each step was carefully executed to ensure high availability, security, and cost-effectiveness.

*Insert Image Here*: **Final overview of the resource group showing all configured resources (resource group, VNet, NSG, and VMs).**

