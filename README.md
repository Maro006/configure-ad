<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This project serves as a demonstrative showcase of adept system administration skills, illustrating proficiency in constructing and managing complex network environments. By meticulously configuring a Microsoft Server to host Active Directory and deploying a Domain Controller, the undertaking underscores adeptness in system architecture and domain management.


The utilization of PowerShell scripting to automate user creation processes showcases a nuanced understanding of automation tools, streamlining administrative tasks and enhancing efficiency. Moreover, the successful integration of Windows 11 Enterprise and the Microsoft Server 2022 ISO within a VMWare virtualized environment underscores adaptability and proficiency in deploying contemporary technologies.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Resources
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in AD
- join Client-1 to your domain (myadproject.com)
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Configuration Steps</h2>


<h3>Setup Resources in Azure </h3>

  - Create the Domain Controller VM (Windows Server 2022) named “DC-1”:
<img width="1400" height="761" alt="image" src="https://github.com/user-attachments/assets/0eb1b642-a99d-4b6f-a7c1-fda3e1ea0225" />
<img width="1400" height="759" alt="image" src="https://github.com/user-attachments/assets/7b574b7b-0264-4003-b532-3416d84ec965" />

  - Using the same Resource Group and Vnet that was created in the previous step create the Client VM (Windows 10) named “Client-1”

<img width="1400" height="760" alt="image" src="https://github.com/user-attachments/assets/c2c37ffd-e51a-4352-8e94-c3c03504dfb6" />

  - Set Domain Controller’s NIC Private IP address to be static

<img width="1400" height="768" alt="image" src="https://github.com/user-attachments/assets/10608072-450b-404a-b340-087e498e85e1" />

  - Ensure that both VMs are in the same Vnet (verify the topology with Network Watcher)

<img width="1400" height="763" alt="image" src="https://github.com/user-attachments/assets/1ec98051-f6b3-4bb1-a082-0d3200d247f2" />

<h3>Ensure Connectivity between the client and Domain Controller</h3>

  - Step 1: Login to Client-1 with Remote Desktop
  - Step 2: Ping DC-1’s private IP address with ping -t (perpetual ping)
<img width="1400" height="599" alt="image" src="https://github.com/user-attachments/assets/cf9bcfc5-7fce-4dc2-beed-94848c32a4f5" />

  - Step 1: Login to the Domain Controller (DC)
  - Step 2: Enable ICMPv4 on the local windows firewall
<img width="1400" height="762" alt="image" src="https://github.com/user-attachments/assets/7e8e3648-e910-4dcc-9331-0a12dc7489a6" />

  - Check Client-1 to verify the ping was successful

<img width="1400" height="601" alt="image" src="https://github.com/user-attachments/assets/d8ab1eda-332e-4a84-b5ea-bc838b06d64f" />

<h3> Install Active Directory </h3>
  - Step1: Login to DC-1
  - Step 2: Install Active Directory Domain Services (ADDS)
<img width="1400" height="835" alt="image" src="https://github.com/user-attachments/assets/91cb3424-60db-43cf-8a1a-8683bd619761" />


  - Promote as a Domain Controller

<img width="1400" height="839" alt="image" src="https://github.com/user-attachments/assets/aa9a7efb-3200-4267-a1a8-f528c520fd74" />

  - Setup a “New Forest” as myactivedirectory.com

<img width="1400" height="836" alt="image" src="https://github.com/user-attachments/assets/d979315c-c70d-41d6-ba0f-32aaef17da1d" />

  - Restart and then log back into DC-1 as user: myadproject.com\labuser:

<img width="1214" height="632" alt="image" src="https://github.com/user-attachments/assets/79484e9c-06e3-412a-a972-e53a772780fc" />

<h3> Create an Admin and Normal User Account in AD </h3>
  - Step 1: Open Active Directory Users and Computers (ADUC)
  - Step 2: Create an Organizational Unit (OU) called “_EMPLOYEES”
  - Step 3: Create an OU called “_ADMINS”:
<img width="1400" height="836" alt="image" src="https://github.com/user-attachments/assets/325f30b2-683a-4199-b961-732e3758e6d5" />

<img width="1400" height="840" alt="image" src="https://github.com/user-attachments/assets/42de5713-3c53-4cc6-ae4f-53dfdc5a0d31" />

Create a new employee named “Jane Doe” with the username of “jane_admin”:

<img width="1400" height="972" alt="image" src="https://github.com/user-attachments/assets/056bc38f-9233-48d5-80e6-4d0a21650082" />

  - Add jane_admin to the “Domain Admins” Security Group

<img width="1400" height="901" alt="image" src="https://github.com/user-attachments/assets/9a609feb-37f4-49db-804f-4a8a5dbeeff8" />

 - Step 1: Log out and close the Remote Desktop connection to DC-1
 - Step 2: Log back in as “myadproject.com\jane_admin”
 - Step 3: Use jane_admin as your admin account from this point on:
<img width="1214" height="620" alt="image" src="https://github.com/user-attachments/assets/0ede0059-0ebf-43d0-8bc8-ca11e799b43c" />

<h3> Join Client-1 to the domain (myadproject.com) </h3>
  - Step 1: Go to the Azure Portal (portal.azure.com)
  - Step 2: Set Client-1’s DNS settings to the DC’s Private IP address:
<img width="1400" height="761" alt="image" src="https://github.com/user-attachments/assets/f90955ad-84d3-4625-9116-60c2c8067d1c" />

  - Step 1: Restart Client-1 from the Azure Portal
  - Step 2: Login to Client-1 (Remote Desktop) as the original local admin (labuser)
  - Step 3: Join it to the domain (computer will restart):
<img width="1400" height="835" alt="image" src="https://github.com/user-attachments/assets/e8619206-ae04-4c61-9bd2-a4be9cf2fb47" />

  - Step 1: Login to the Domain Controller (Remote Desktop)
  - Step 2: Verify that Client-1 is viewable in Active Directory Users and Computers (ADUC) inside the “Computers” container on the root of the domain
  - Step 3: Create a new OU named “CLIENTS”
  - Step 4: Move Client-1 to the new OU
<img width="1400" height="847" alt="image" src="https://github.com/user-attachments/assets/fd954a92-833e-451b-81f4-cff1f465d46a" />

<h3> Setup Remote Desktop for non-administrative users on Client-1 </h3>
  - Step 1: Log into Client-1 as mydomain.com\jane_admin
  - Step 2: Open system properties
  - Step 3: Click “Remote Desktop”
  - Step 4: Allow “domain users” access to remote desktop
  You can now log into Client-1 as a normal, non-administrative user now.

  - Normally you’d want to do this with Group Policy that allows you to change MANY systems at once.

<img width="1400" height="835" alt="image" src="https://github.com/user-attachments/assets/679f9ff4-316e-457e-9b7e-c17ae326fb3b" />

<h3> Create a bunch of additional users and attempt to log into client-1 with one of the users </h3>
  - Step 1: Login to DC-1 as jane_admin
  - Step 2: Open PowerShell_ise as an administrator
  - Step 3: Create a new File
  - Step 4: Paste the contents of the script into the newly created file 
<img width="1400" height="814" alt="image" src="https://github.com/user-attachments/assets/13ffe20f-09b2-474c-8abb-0ebf19baee5e" />

  - Step 1: Run the script
  - Step 2: Observe the accounts being created
<img width="1400" height="833" alt="image" src="https://github.com/user-attachments/assets/e5951bdb-c5af-484b-9a26-d1836b60ac92" />

  - Step 1: Open ADUC
  - Step 2: Observe the accounts in the appropriate OU
  - Step 3: Attempt to log into Client-1 with one of the accounts (take note of the password in the script)
<img width="1400" height="848" alt="image" src="https://github.com/user-attachments/assets/b849e742-139b-4fd0-908e-241c40b39ad0" />

<img width="1184" height="638" alt="image" src="https://github.com/user-attachments/assets/6a2211da-bfa1-4cec-8657-926613f5f82c" />


