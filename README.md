<p align="center">
<img width="450" height="250" alt="Microsoft Active Directory Logo" src="https://github.com/user-attachments/assets/cd75c7f5-fba1-4682-a616-dc487e761fbc"
 alt="Microsoft Active Directory Logo"/>
</p>

<h1>Deploying and Configuring Active Directory in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Prerequisites</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/joshuaheck1/VM-creation)
  (Reference this project for help creating Virtual Manchines if needed.)
  
- [Create Active Directory Infrastructure in Azure](https://github.com/joshuaheck1/create-ad-infrastructure)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Wndows App (for MacOS)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Install Active Directory
- Step 2: Create a Domain Admin User within the Domain
- Step 3: Join Client-1 to the Domain
- Step 4: Setup Remote Desktop for non-admin users on Client-1

<h2>Deployment and Configuration Steps</h2>

<h3>Step 1: Install Active Directory</h3>
<p>
<img width="800" alt="DAD1" src="https://github.com/user-attachments/assets/e448cbc4-30a5-433c-8730-f2a1acccc464" />
</p>

<p>
- Login into DC-1 via Remote Desktop.
<p>- In Server Manager, select "Add roles and features" and click Next.</p>
<br />

<p>
<img width="800" alt="DAD2" src="https://github.com/user-attachments/assets/6c183f05-52e8-44d7-94d9-cd2dbd424be0" />
</p>

<p>
- Select the destination server and click Next. (Only one should be listed, our DC-1).
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
