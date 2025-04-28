<p align="center">
<img width="450" height="250" alt="Microsoft Active Directory Logo" src="https://github.com/user-attachments/assets/cd75c7f5-fba1-4682-a616-dc487e761fbc"
 alt="Microsoft Active Directory Logo"/>
</p>

<h1>Deployment and Configuration of Active Directory in the Cloud</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Prerequisites</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/joshuaheck1/VM-creation)
  
- [Create Active Directory Infrastructure in Azure](https://github.com/joshuaheck1/create-ad-infrastructure)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Wndows App (for macOS)
- Remote Desktop
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- macOS Sequoia
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
 - Under "Select the deployment operation", select Add a new forest and name it mydomain.com -> click Next.
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
<p>- Once the install is finished, DC-1 will reboot. This might take a couple minutes because DC-1 is now on the domain.</p>
<br />

<p>
<img width="800" alt="Screenshot 2025-04-23 at 1 12 32 AM" src="https://github.com/user-attachments/assets/77357c2e-c68f-4366-af58-6acca7881af0" />
</p>
<p>
 - Remote Desktop back into DC-1. Since DC-1 is now a domain controller and on the domain, you have to specify which domain, and that you want to log on as a domain user.</p>  
<p>- Enter "mydomain.com\jheck1" (mydomain.com\username)</p>
<p>- This will log us in as a specific user within the domain.</p>
<br />

<h3>Step 2: Create a Domain Admin User within the Domain</h3>

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

<p>
<img width="800" alt="DAD17" src="https://github.com/user-attachments/assets/9cf665b5-72a9-4e36-a53a-bb5049b07ce3" />
</p>
<p>
 - Now, right-click mydomain.com and select Refresh. This will move our new OUs to the top of the list for easier location and access.</p>  
<br />

<p>
<img width="800" alt="DAD18" src="https://github.com/user-attachments/assets/86ae7e0f-d9e2-4a81-8bba-ec6066f5d7b0" />
</p>
<p>- Next, we will create a new user.</p> 
 <p>- Right-click _ADMINS -> select New -> click User.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD19" src="https://github.com/user-attachments/assets/4848b413-6391-40f2-bdb4-d9d79531988b" />
    </td>
    <td>
      <img width="1000" alt="DAD20" src="https://github.com/user-attachments/assets/1fbf670b-c6bb-4683-b57e-e3ad8e4e6155" />
    </td>
  </tr>
</table>
<p>- Name the new user "Jane Doe" with the username "jane_admin" and click Next.</p>
<p>- Use the same password as DC-1 to keep it simple. Uncheck "User must change password at next login" and check "Password never expires". (We wouldn't do this in the real world for security purposes, but its ok for this project 😉).</p>
<br />

<p>
<img width="500" height="400" alt="DAD21" src="https://github.com/user-attachments/assets/a972929d-c10a-4b24-b6d8-d9261fba05bc" />
</p>
<p>- Confirm the new user's information and click Finish.</p> 
<br />

<p>
<img width="800" alt="DAD23" src="https://github.com/user-attachments/assets/a8c61736-e95a-4adf-97f3-2f5cf010920c" />
</p>
<p>- Now, we will make "Jane Doe" a Domain Admin by adding this account to the built-in "Domain Admins" Security Group. </p> 
<p>- Open the _ADMINS folder -> right-click Jane Doe -> select Properties.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD24" src="https://github.com/user-attachments/assets/e57fd05a-6735-448f-b1a9-87ac0b7768a5" />
    </td>
    <td>
      <img width="1000" alt="DAD25" src="https://github.com/user-attachments/assets/229ab0d9-183a-4267-9868-a0ba8d777a03" />
    </td>
  </tr>
</table>
<p>- Select "Member of" and click "Add".</p>
<p>- Type in "domain admins" and click "Check Names".</p>
<p>- Notice that after clicking "Check Names", "Domain Admins" is now capitalized and underlined. Click OK. (See figure 23)</p>
<br />

<p>
<img width="460" height="450" alt="DAD26" src="https://github.com/user-attachments/assets/9059c515-51f3-4185-b626-cb3b2f368e06" />
</p>
<p>- We can confirm that Jane Doe is now a Domain Admin. The Force is strong with this one!🧘🏽‍♀️ (Click OK).</p>
<p>- Next, we will log out and close the DC-1 connection. Then, we will log back into DC-1 with Jane Doe's Admin login and we'll use this account from now on. (Note Jane Doe's login info)</p>
<br />

<h3>Step 3: Join Client-1 to the Domain</h3>

<p>
<img width="800" alt="DAD28" src="https://github.com/user-attachments/assets/6f9d0f46-f77e-4a4e-957d-20031cd8eaaa" />
</p>
<p>- Now, we will login to Client-1 as the original local admin. (jheck1) </p>
<p>- Right-click Start Menu -> select System </p>
<p>- Take a second and look over Figure 25. There is alot going on here and the windows pop-up in a weird order. </p>
<p>- 1. Select "Rename this PC (advanced)". If you don't see this option at first, maximze the window or expand it to the right a little.</p>
<p>- 2. In the "Computer Name" tab, click "Change".</p>
<p>- 3. Under "Member of" select "Domain" and type in mydomain.com. </p>
<p>- 4. Click OK.</p>
<br />


<p>
<img width="800" alt="DAD29" src="https://github.com/user-attachments/assets/2bea523f-637c-4d03-9bfd-58d63b6f712d" />

</p>
<p>- To join the domain, we will use the jane_admin account. </p>
<p>- Enter in mydomain.com\jane_admin and password. click OK. </p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD30" src="https://github.com/user-attachments/assets/b3fdd933-ddad-4be7-8dd5-de8ae77682ee" />
    </td>
    <td>
      <img width="1000" alt="DAD31" src="https://github.com/user-attachments/assets/b2f1a5ce-f789-46e6-8c98-e69f62383f15" />
    </td>
  </tr>
</table>
<p>- Once you clicked OK, the pop-up happened behind the System screen. Close that and you will see it as in Figure 27.</p>
<p>- Click OK.</p>
<p>- Client-1 will need to restart. Click Restart Now.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD33" src="https://github.com/user-attachments/assets/101b154b-33f6-4f94-a8ea-193d61e045a7" />
    </td>
    <td>
      <img width="1000" alt="DAD34" src="https://github.com/user-attachments/assets/c26e0870-57d4-488b-a383-c9e47ec09d3d" />
    </td>
  </tr>
</table>
<p>- We will go to DC-1 now. If you just closed the connection earlier, simply log back in using the jane_admin account. (mydomain.com\jane_admin) </p>
<p>- From the Start Menu -> Active Directory Users and Computers (ADUS). </p>
<p>- Expand mydomain.com -> select Computers. We can verify Client-1 is here and successfully joined the domain. Figure 29</p>
<p>- Now, we will create a new OU named _CLIENTS</p>
<p>- Right-click mydomain.com -> select New -> click Organizational Unit</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="DAD36" src="https://github.com/user-attachments/assets/4cd8b573-cfee-42e6-8df2-59d4a8242d24" />
    </td>
    <td>
      <img width="1000" alt="DAD37" src="https://github.com/user-attachments/assets/774bf3c8-40aa-4b6b-a3c5-8ef40cbac197" />
    </td>
  </tr>
</table>
<p>- Go back to Computers and drag Client-1 to the new _CLIENTS OU. </p>
<p>- Click Yes on the pop-up. You can Refresh mydomain.com to move _CLIENTS to the top with _ADMINS & _EMPLOYEES if you want.</p>
<br />

<h3>Step 4: Setup Remote Desktop for non-admin users on Client-1</h3>

<p>
<img width="500" height="400" alt="Screenshot 2025-04-23 at 11 21 16 AM" src="https://github.com/user-attachments/assets/147451a6-923c-4f87-b233-f63051053e16" />
</p>
<p>- Login into Client-1 with the jane_admin account.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="RD1" src="https://github.com/user-attachments/assets/4c7f51ab-4d66-42fd-a001-23bbf927603a" />
    </td>
    <td>
      <img width="1000" alt="RD2" src="https://github.com/user-attachments/assets/9b9e27b9-11d0-4721-8709-a6a4dffb6a28" />
    </td>
  </tr>
</table>
<p>- Right-click Start Menu -> select System -> click Remote Desktop. </p>
<p>- In Remote Desktop Users, click Add. </p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="RD3" src="https://github.com/user-attachments/assets/f6115248-d541-4fe0-8d65-9dacfaf79815" />
    </td>
    <td>
      <img width="1000" alt="RD4" src="https://github.com/user-attachments/assets/ac7c5331-de75-4065-8c37-8e8d62cd4ac0" />
    </td>
  </tr>
</table>
<p>- Type in domain users and click Check Names. Domain Users will capitalize and be underlined. Click OK. </p>
<p>- Confirm that MYDOMAIN\Domain Users is showing under Remote Desktop Users and click OK. </p>
<p>- Now, all users in the Domain Users group can Remote Desktop into Client-1. </p>
<br />

<h2>Conclusion</h2>

<p>This concludes our project. We did it! AD has been successfully deployed. We will add a bunch of users next. Don't forget to Stop (turn off) the VMs in Azure. As always, Thank You for your time and viewing this Project. We'll see you on the next one! 😎      
</p>
<br />





