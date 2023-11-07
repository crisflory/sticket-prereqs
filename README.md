<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Create Resource Group
- Create Azure Virtual Machine
- Enable IIS
- Install PHP
- Install My SQL
- Install OsTicket

Start by creating a Resource Group.
Proceed to create a Windows 10 Virtual Machine (VM) with 2-4 Virtual CPUs. When setting up the VM, allow it to create a new Virtual Network (Vnet).
Part 2 (Installation)

Note: This is more than just a simple list; it outlines the steps for installing various prerequisite software. You can use it as a guide without needing to memorize the details.

Begin by creating an Azure Virtual Machine with Windows 10 and 4 vCPUs.

Name: Vm-osticket
Username: labuser (customize as needed)
Password: osTicketPassword1! (customize as needed)


Install/Enable IIS in Windows with the following features:

CGI and Common HTTP Features
World Wide Web Services -> Application Development Features
->CGI
 ->Common HTTP Features
Internet Information Services -> Web Management Tools
-> IIS Management Console Management
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/5a049364-a58e-4799-a296-24075318a980)


Download and install "PHP Manager for IIS" 
Download and install the "Rewrite Module" 

Create a directory at C:\PHP.

Download PHP version 7.3.8 and unzip its contents into C:\PHP.

If prompted, choose to "Keep" the file.

If you encounter difficulties downloading PHP 7.3.8, consider installing Google Chrome and attempting the download from there.

Download and install VC_redist.x86.exe.

Download and install MySQL 5.5.62.

Choose the "Typical Setup" option.
Launch the Configuration Wizard after installation.
Opt for the "Standard Configuration" and set the password to "Password1".
Open IIS as an Administrator.

Register PHP from within IIS.

Reload IIS (Open IIS, stop and start the server).

Install osTicket v1.15.8:

Download osTicket
Extract and copy the "upload" folder to C:\inetpub\wwwroot.
Rename the "upload" folder to "osTicket" within C:\inetpub\wwwroot.
Reload IIS (Open IIS, stop and start the server).
Access the osTicket site at sites -> Default -> osTicket.
Click "Browse *:80".
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/50d0e111-65a2-4268-93d7-e2d46e669e57)

Note that some extensions are not enabled.
Go back to IIS, sites -> Default -> osTicket.
Double-click PHP Manager.
Click "Enable or disable an extension".
Enable: php_imap.dll, php_intl.dll, and php_opcache.dll.
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/ed5cb488-7b09-4913-9583-24fe23d5fda1)

Refresh the osTicket site in your browser to observe the changes.
Rename "ost-config.php" from C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php to C:\inetpub\wwwroot\osTicket\include\ost-config.php.

Assign permissions to "ost-config.php":

Disable inheritance and remove all permissions.
Add new permissions for everyone with "All" access.
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/e38273f8-ae13-4302-9c40-ffd448dde467)
Continue setting up osTicket in the browser (click "Continue").
Name your Helpdesk.
Specify the default email (which receives customer emails).
Download and install HeidiSQL.
Open HeidiSQL.
Create a new session using "root" and "Password1".
Connect to the session.
Create a database named "osTicket".
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/2b2d246b-6cf5-4efa-9c28-ea6a1e5c380d)
Continue setting up osTicket in the browser:
Specify the MySQL Database as "osTicket".
Enter the MySQL Username as "root".
Set the MySQL Password as "Password1".
Click "Install Now!"
Congratulations! Hopefully, the installation went smoothly.
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/a896525c-face-46e6-84d5-dd7df4a4ddc2)

Access your help desk login page: http://localhost/osTicket/scp/login.php.
End Users osTicket URL:
http://localhost/osTicket/

Clean up:

Delete: C:\inetpub\wwwroot\osTicket\setup.
Set permissions for "ost-config.php" to "Read" only: C:\inetpub\wwwroot\osTicket\include\ost-config.php.
Notes:

Access your help desk login page: http://localhost/osTicket/scp/login.php.
End Users osTicket URL: http://localhost/osTicket/.
Part 3 (Post Installation Setup)

Configure Roles:

In the Admin Panel, navigate to Agents -> Roles.
Create a "Supreme Admin" role.
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/adb05839-8937-413f-a4e8-0ba05906ca31)

Configure Departments:

In the Admin Panel, go to Agents -> Departments.
Configure the "System Administrators" department.
Configure Teams:

In the Admin Panel, access Agents -> Teams.
Create "Level I Support" and "Level II Support" teams.
Allow anyone to create tickets:

In the Admin Panel, go to Settings -> User Settings.
Set "Registration Required" to "Require registration and login to create tickets."

Configure Agents (workers):
In the Admin Panel, navigate to Agents -> Add New.
Add two agents of your name of choice.
Configure Users (customers):

In the Agent Panel, go to Users -> Add New.
Add two users with different names than your agents that you added.
![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/8fe05f32-e5a7-4049-abcc-3ec54880ddcd)

Configure SLA:

In the Admin Panel, access Manage -> SLA.
Set up service level agreements: "Sev-A" (1 hour, 24/7), "Sev-B" (4 hours, 24/7), and "Sev-C" (8 hours, business hours).
Configure Help Topics:

In the Admin Panel, go to Manage -> Help Topics.
Configure help topics: "Business Critical Outage," "Personal Computer Issues," "Equipment Request," and "Password Reset."
Part 4 (Tickets and Ticket Lifecycle)

![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/6bd28262-1886-4670-a5ed-660a57613392)

Practice creating, triaging, and solving tickets. For guidance on handling multiple tickets, consider watching instructional videos. Here are some ticket examples:

![image](https://github.com/crisflory/osticket-prereqs/assets/147748310/6ea74019-ec1a-401e-af91-f74290d4be16)

Sev-A (1 hour, 24/7) [entire mobile/online banking system is down] -> Assign to SysAdmins.
Sev-B (4 hours, 24/7) [accounting department needs Adobe upgrade, broken].
Sev-B/C (2 hours, business hours) [CFO’s laptop seems a bit slow].





