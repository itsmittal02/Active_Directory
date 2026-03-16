# Active_Directory




Active Directory Implementation & User Management
Project Explanation (Step-by-Step with Configuration)
1. Environment Setup

First, we prepared the environment where Active Directory would run.

Requirements

Windows Server (2016 / 2019 / 2022)

Static IP configuration

System connected to network

Steps

Install Windows Server on the machine.

Configure Static IP Address

Go to:

Control Panel → Network & Internet → Network Connections → Ethernet → Properties → IPv4

Example configuration:

IP Address: 192.168.1.10
Subnet Mask: 255.255.255.0
Gateway: 192.168.1.1
Preferred DNS: 192.168.1.10

Reason:
Active Directory requires a static IP and DNS service.

2. Installing Active Directory Domain Services (AD DS)

Active Directory works through a role called AD DS.

Steps

Open Server Manager

Click Add Roles and Features

Choose Role-based Installation

Select the server

Select:

Active Directory Domain Services

Click Add Features

Click Next → Install

After installation, a notification appears.

3. Promote Server to Domain Controller

After installing AD DS, the server must be promoted to a Domain Controller.

Steps

Click the notification flag in Server Manager

Select:

Promote this server to a domain controller

Choose:

Add a new forest

Example Domain Name:

company.local
or
corp.local

Set Directory Services Restore Mode (DSRM) password

Example:

Admin@123

Keep default settings and click Install

The server will restart automatically.

Now the system becomes a Domain Controller.

4. Creating Organizational Units (OU)

OU helps organize users and computers.

Example company structure:

Company
│
├── HR
├── IT
├── Finance
└── Sales

Steps

Open:

Tools → Active Directory Users and Computers

Right click on domain

Select:

New → Organizational Unit

Example:

OU Name: IT
OU Name: HR

This helps manage policies department-wise.

5. Creating User Accounts

Now we create users inside OUs.

Steps

Go to:

Active Directory Users and Computers

Select OU (Example: IT)

Right click → New → User

Example user:

First Name: Rahul
Last Name: Sharma
User Logon Name: rahul.sharma

Password:

Temp@123

Options:

☑ User must change password at next login

Click Finish.

6. Creating Security Groups

Groups help manage permissions easily.

Example groups:

IT_Admin

HR_Team

Finance_Team

Steps

Right click OU

Select:

New → Group

Example:

Group Name: IT_Admin
Group Scope: Global
Group Type: Security

Add users to group:

Group → Properties → Members → Add

7. Implementing Group Policy (GPO)

Group Policy allows administrators to control user settings and security.

Examples:

Password policy

Desktop restrictions

USB blocking

Software restrictions

Steps

Open:

Server Manager → Tools → Group Policy Management

Right click Domain

Select:

Create a GPO

Example:

GPO Name: Password Policy

8. Configure Password Policy

Inside Group Policy Editor:

Go to:

Computer Configuration
→ Policies
→ Windows Settings
→ Security Settings
→ Account Policies
→ Password Policy

Configure:

Minimum password length = 8
Password complexity = Enabled
Password history = 5
Maximum password age = 30 days

Apply policy.

9. User Permissions & Access Control

We assign permissions to users or groups.

Example:

IT team → full access to servers

HR team → HR folder access

Steps

Right click folder → Properties → Security → Edit → Add

Add:

IT_Admin group

Permission:

Full Control

10. Managing Users (Daily Administration)

Typical admin tasks:

Disable user

Right click user → Disable account

Reset password

Right click user → Reset password

Unlock account

User → Properties → Unlock account

Move user to different OU

Drag and drop user.

11. Testing User Login

Now test domain authentication.

On client machine:

Join computer to domain.

Steps:

System Properties → Computer Name → Change

Select:

Domain: company.local

Login example:

company\rahul.sharma

If login successful → AD configuration works.

12. Monitoring & Maintenance

Admin regularly checks:

Event Viewer logs

Group policy updates

Account lockouts

Security settings

Command used:

gpupdate /force

This forces policy update.
