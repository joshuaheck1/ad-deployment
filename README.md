<p align="center">
<img width="450" height="250" alt="Microsoft Active Directory Logo" src="https://github.com/user-attachments/assets/cd75c7f5-fba1-4682-a616-dc487e761fbc"
 alt="Microsoft Active Directory Logo"/>
</p>

<h1>Deployment and Configure Active Directory in the Cloud (Azure)</h1>
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

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD3" src="https://github.com/user-attachments/assets/ff9d92da-e5ff-42b4-909f-74830be3e249" />
    </td>
    <td>
      <img width="1000" alt="DAD4" src="https://github.com/user-attachments/assets/2d876eea-6b39-4958-bdda-62fc94070b81" />
    </td>
  </tr>
</table>
<p>
 - For Server Roles, select Active Directotry Domain Services (ADDS) and click Add Features.
<p> - Confirm the box is checked next to ADDS and click Next.</p>
<br />

<p>
<img width="800" alt="DAD5" src="https://github.com/user-attachments/assets/38137c49-ed14-42fa-a5d2-22581ef9b503" />
</p>
<p>
 - Check the box next to Restart the destination server automatically if required. Click Yes on the pop-up and click Install.
<p> - Once the Feature installation finishes, simply click Close.</p>
<br />

<p>
<img width="800" alt="DAD7" src="https://github.com/user-attachments/assets/d15cbaa1-35a8-47dc-80fa-e81db8cba77f" />
</p>

<p>
- Now, locate the flag and yellow tringle at the top right of the sreen in Server Manager and click on it.
</p>
<p>- Next, select Promote this server to a domain controller.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD8" src="https://github.com/user-attachments/assets/59bd513e-b628-44f3-9cb4-9a83cfc6989d" />
    </td>
    <td>
      <img width="1000" alt="DAD9" src="https://github.com/user-attachments/assets/55e038e6-f13b-4388-bb5a-e13f3d33baa2" />
    </td>
  </tr>
</table>
<p>
 - Under "Select the deployment opertion", select Add a new forest and name it mydomain.com -> click Next.
<p> - For the DSRM password, just use Password1. We will not use this at all. Click Next.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD10" src="https://github.com/user-attachments/assets/64d0adad-2493-4946-a741-bc42363c0b97" />
    </td>
    <td>
      <img width="1000" alt="DAD11" src="https://github.com/user-attachments/assets/7227030b-594e-484d-8e0c-dd27fa9b9670" />
    </td>
  </tr>
</table>
<p>
 - Uncheck the DNS delegation options and click Next. Keep clicking Next for the next couple on options until you see Figure 10.
<p> - Now that all the options have been configured, click Install to begin installation.</p>
<p>- Once the install is finished, DC-1 will reboot.</p>
<br />

<p>
<img width="800" alt="Screenshot 2025-04-23 at 1 12 32 AM" src="https://github.com/user-attachments/assets/77357c2e-c68f-4366-af58-6acca7881af0" />
</p>
<p>
 - Now, Remote Desktop back into DC-1. Be sure to specify the domain in the username because DC-1 is a Domain Controller now. Enter "mydomain.com\jheck1" (mydomain.com\username)
<p> - This will log us in as a specific user with the domain.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD13" src="https://github.com/user-attachments/assets/bef99c17-6550-48ac-9366-2466879d57e9" />
    </td>
    <td>
      <img width="1000" alt="DAD14" src="https://github.com/user-attachments/assets/b8e40402-5612-44f1-868d-53c6dfc0e55d" />
    </td>
  </tr>
</table>
<p>
 - Once you are back in DC-1, from the Start Menu -> select Windows Administrative Tools -> open Active Directory Users & Computers.
<p> - Here we will create a new Organizational Unit (OU). </p>
<p>- Right-click mydomain.com -> New -> Organizational Unit. Name this OU as _EMPLOYEES (don't forget the underscore). Click OK.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD15" src="https://github.com/user-attachments/assets/300ef3de-f8ed-4e94-8938-46ade24aaef8" />
    </td>
    <td>
      <img width="1000" alt="DAD16" src="https://github.com/user-attachments/assets/756394d7-c8dc-4a37-9ecd-108c50dff317" />
    </td>
  </tr>
</table>
<p>- We will need to create another new Organizational Unit (OU).</p>
<p>- Right-click mydomain.com -> New -> Organizational Unit. Name this OU as _ADMINS (don't forget the underscore). Click OK.</p>
<br />










