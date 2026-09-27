# Domain-Controller-with-Active-Directories
Windows Server 2022: Domain Controller & Active Directory Setup Guide 

- Objective: Configure a Windows Server 2022 environment as a Domain Controller by setting up network adapters, assigning a static IP address, and installing/promoting Active Directory Domain Services (AD DS). 
- Prerequisites: 
  - Windows Server 2022 Standard Evaluation installed. 
  - Oracle VM VirtualBox environment. 
  - Administrative privileges.
  
Step 1: Configure Virtual Network Adapters

Set up the virtual machine network settings to allow isolated host communication necessary for a domain testing environment.
- Action: In VirtualBox, open the settings for the Windows Server VM. Navigate to the Network menu, select Adapter 1, enable it, and attach it to a Host-only Adapter (VirtualBox Host-Only Ethernet Adapter).
- Proof:

  <img width="778" height="511" alt="Configure Network Adapter" src="https://github.com/user-attachments/assets/72e58b3c-bf53-49ca-a036-48e887f916c2" />

Step 2: Assign a Static IP Address

A Domain Controller requires a reliable, fixed network identity to properly manage domain lookups and DNS queries.
- Action: Access Network Connections on the server. Open the properties for your host-only Ethernet adapter, navigate to Internet Protocol Version 4 (TCP/IPv4) Properties, and manually configure the following parameters:
  - IP address: 192.168.56.10
  - Subnet mask: 255.255.255.0
  - Preferred DNS server: 192.168.56.10 (points to itself for domain DNS resolution)
- Proof:

<img width="1024" height="768" alt="Static IP address" src="https://github.com/user-attachments/assets/e1a95a58-ca97-4374-97a0-c1d1f3e877e5" />

Step 3: Verify the Static IP Address Configuration

Confirm that the operating system has accurately applied your custom network parameters.
- Action: Open the Command Prompt as an Administrator and execute the command ipconfig. Ensure that Ethernet adapter Ethernet accurately reports the IPv4 address 192.168.56.10 and Subnet Mask 255.255.255.0.
- Proof:

<img width="1024" height="768" alt="Check IP" src="https://github.com/user-attachments/assets/870f848f-f5a8-4308-926e-6a40b9000937" />

Step 4: Install Active Directory Domain Services (AD DS)

Deploy the core Active Directory roles to prepare the server for promotion to a domain controller.
- Action: Open Server Manager, select Add Roles and Features, and proceed through the wizard to select and install Active Directory Domain Services along with its default management tools and dependencies.
- Proof:

<img width="1024" height="768" alt="Install Active Directory" src="https://github.com/user-attachments/assets/f8c3c6ce-9854-4f7d-a8e8-e569e8bff42f" />

Step 5: Promote the Server to a Domain Controller

After the binary files finish installing, the server must be promoted to activate the domain functionality.
- Action:Click the Notification Flag (yellow warning triangle icon) in the top-right corner of Server Manager.Click Promote this server to a domain controller.In the Deployment Configuration wizard, choose Add a new forest and type the root domain name: LAB.local.Set your Directory Services Restore Mode (DSRM) password, proceed through the remaining default options, and click Install.The server will automatically reboot to finalize the configuration.
- Proof: (Process step verified textually via the successful root environment check in Step 6).

Step 6: Confirm Active Directory Installation and Domain Status

Verify that the domain controller role is active and accessible via management utilities.
- Action: After the system reboots, log in with your administrator account. Open Server Manager, click Tools in the upper-right corner, and select Active Directory Users and Computers. Verify that your custom domain tree (LAB.local) displays correctly in the root folder structure.
- Proof:

<img width="1024" height="768" alt="Confirm Active directory is running" src="https://github.com/user-attachments/assets/31a3c40f-aac9-4744-8c0b-1bfee56f4228" />
