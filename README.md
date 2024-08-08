<p align="center">
<img src="https://i.imgur.com/4hzgUaF.jpeg" alt="Azure logo"/>
</p>

<h1>Lab - Azure Active Directory</h1>

- Simple Steps and Description:

We'll set up a system called Active Directory on a cloud server. This helps manage users and computers in a network.

- Create a Domain Controller: Make a Windows Server in the cloud to manage the network.
- Create a Client Computer: Make a Windows 10 computer in the cloud to join the network.
- Install Active Directory: Set up Active Directory on the server.
- Create User Accounts: Make accounts for different users.
- Join the Client Computer to the Domain: Connect the Windows 10 computer to the network

This lab focuses on deploying Active Directory in an Azure environment. You'll set up a Domain Controller and a client machine, configure Active Directory Domain Services, create user accounts, and join the client machine to the domain. This project helps you gain practical experience in managing and deploying Active Directory for user and resource management. <br />

<h2>Environments and Technologies Used</h2>

- Azure Portal
- Windows Server 2022 VM (Domain Controller)
- Windows 10 VM (Client)
- Active Directory Domain Services (AD DS)
- PowerShell

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Installation Steps</h2>

- Part 1: Setup Resources in Azure

- Create Domain Controller VM:

In the Azure Portal, create a Windows Server 2022 VM named DC-1.
Set the NIC Private IP address to static.
- Create Client VM:

Create a Windows 10 VM named Client-1 in the same Resource Group and Vnet.
- Ensure Connectivity:

Ensure both VMs are in the same Vnet using Network Watcher.
Log into Client-1 using Remote Desktop.
Ping DC-1's private IP address with the command ping -t <DC-1-IP>.
Part 2: Install Active Directory
- Install AD Domain Services:

Log into DC-1 using Remote Desktop.
Open "Server Manager", navigate to "Manage" -> "Add Roles and Features".
Select "Active Directory Domain Services" and install it.
- Promote to Domain Controller:

After installation, click on the notification flag in "Server Manager" and promote the server to a domain controller.
Set up a new forest with the domain name (e.g., mydomain.com).
Restart DC-1 and log back in as mydomain.com\labuser.
- Create Admin and User Accounts:

Open "Active Directory Users and Computers" (ADUC).
Create Organizational Units (OUs) _EMPLOYEES and _ADMINS.
Create an admin user jane_admin with the same password and add to "Domain Admins".
- Part 3: Join Client-1 to the Domain
- Set DNS and Join Domain:

In the Azure Portal, set Client-1's DNS settings to DC-1's private IP address.
Restart Client-1.
Log into Client-1 as the local admin (labuser) and join it to the domain (mydomain.com).
- Verify in ADUC:

Log into DC-1 and open ADUC.
Ensure Client-1 shows up in the "Computers" container.
(Optional) Create an OU _CLIENTS and move Client-1 into it.
Part 4: Setup Remote Desktop for Non-Administrative Users
Allow Remote Desktop Access:
Log into Client-1 as mydomain.com\jane_admin.
Open System Properties, click "Remote Desktop", and allow "domain users" access.
Part 5: Create Additional Users
Create Users with PowerShell Script:
Log into DC-1 as jane_admin.
Open PowerShell ISE as an administrator.
Create a new file, paste the PowerShell script from GitHub, and run it.
Observe the user accounts being created in the appropriate OU.
Test logging into Client-1 with one of the new user accounts.

<img src="https://i.imgur.com/SvW5yyZ.png" alt="Active Directory"/>
