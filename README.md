<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory within Azure VMs Part 2</h1>
This tutorial guides the implementation of Active Directory within Microsoft Azure Virtual Machines. For this tutorial to be completed, you must finish the prerequisites first and come back to this one as it builds upon those.  <br />

<h2>Prerequisites</h2>

[Configuring On-premises Active Directory within Azure VMs Part 1](https://github.com/BenjaminG-Dreams/configure-ad)

<h2>Technologies and Enviroments Used</h2>

- Microsoft Azure
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Create resources in a resource group in Azure
- Ensure Connectivity between the client and Domain Controller
- Install Active Directory
- Create an Admin and Normal User Account in Active Directory
- Join Client-1 to your domain
- Setup Remote Desktop for non-administrative users on Client-1
- Create additional users and attempt to log into client-1 with one of the users

<h2>Deployment and Set Up</h2>


![Screenshot 2025-01-31 195344](https://github.com/user-attachments/assets/2c35b3f6-1aa8-4bae-9501-2f1d3fec32d7)

![Screenshot 2025-01-31 195420](https://github.com/user-attachments/assets/eb1fd3bf-a8b1-42d4-b017-f66265735286)

![Screenshot 2025-01-31 195454](https://github.com/user-attachments/assets/361c9dc3-eb9e-4384-9019-b84acc66f2d2)

![Screenshot 2025-01-31 195539](https://github.com/user-attachments/assets/8c3028a0-00ec-4f33-9a3c-99fb7c62f29a)

![Screenshot 2025-01-31 195652](https://github.com/user-attachments/assets/d986a385-8892-4a89-b325-a7a71ffc6de3)

![Screenshot 2025-01-31 195708](https://github.com/user-attachments/assets/4063a977-6a92-4052-b24e-dfc2e4fbe0ae)

![Screenshot 2025-01-31 195730](https://github.com/user-attachments/assets/27a9ec9e-0b44-4b1d-8d9b-34259eef230a)

![Screenshot 2025-01-31 195826](https://github.com/user-attachments/assets/0369ee99-8d2c-460c-87d0-0096ab9efb79)

<p>
Finally, we will install Active Directory inside of DC-1. Open up DC-1 and click into "Sever Manager". The first thing we will click is "Add roles and features", press next until we get into "Server Roles", check the box that says "Active Directory Domain Services", click "Add Features" and then continue to click next until you can install.
</p>
<br />

![Screenshot 2025-01-31 200032](https://github.com/user-attachments/assets/8afdc546-9ec6-460a-9799-cbdf657b5092)

<p>
Next, we'll promote the DC-1 as a domain controller. To do this we'll click on the flag with the caution sign on the top right of "Server Manager" and press "Promote this server to a domain controller".
</p>
<br />

![Screenshot 2025-01-31 200143](https://github.com/user-attachments/assets/bc02efa3-a39b-446d-ac17-fe1e5a181b2a)

<p>
Next, check "Add a new forest" and name it to anything you want. In this tutorial, we will use "mydomain.com" and hit next. The password doesn't really matter but just write it down just make sure
</p>
<br />

![Screenshot 2025-01-31 200251](https://github.com/user-attachments/assets/0ed8b243-ebc0-4d44-8933-8a44f3482c83)

![Screenshot 2025-01-31 200353](https://github.com/user-attachments/assets/2f94b54f-7101-49b9-ba96-63303f1e24af)

![Screenshot 2025-01-31 200423](https://github.com/user-attachments/assets/5b28e856-4e45-45ec-a492-b1fb55c83311)

![Screenshot 2025-01-31 200500](https://github.com/user-attachments/assets/d9812c87-8d27-44a4-a7e6-9f28390e7604)

![Screenshot 2025-01-31 200619](https://github.com/user-attachments/assets/41f2e949-0c0a-4cdc-8ecd-abe095e6acec)

![Screenshot 2025-01-31 200721](https://github.com/user-attachments/assets/53fafffd-3c34-4150-a705-b06657f32c58)


<p>
Now you can make a DSRM password and hit next until you are able to install. This will restart the virtual machine after it is finished.
</p>
<br />

![Screenshot 2025-01-31 201517](https://github.com/user-attachments/assets/de321249-8e2c-4fb1-9f87-6d74c69cf9b0)

<p>
Next, we'll connect back into "DC-1" with RDC. This time we will use a different account and type the user as "mydomain.com\labuser" or the username that you created when you made "DC-1" The password will be the same.
</p>
<br />

![Screenshot 2025-01-31 201640](https://github.com/user-attachments/assets/dee6abb5-c0b8-4c10-906d-b9652d708377)

<p>
Now we'll go to the server manager and then go to tools. Press "Active Directory Users and Computers" or ADUC.
</p>
<br />

![Screenshot 2025-01-31 202007](https://github.com/user-attachments/assets/f600e3c2-735e-456c-99a6-3c93b5028ac0)

![Screenshot 2025-01-31 202059](https://github.com/user-attachments/assets/a2573f87-f6b8-41e8-96c3-17b1c9d69215)

![Screenshot 2025-01-31 202220](https://github.com/user-attachments/assets/affe01a9-51c5-4a61-81ce-d07fb1720084)


<p>
Next create two new "Organizational Units" by clicking on mydomain and right clicking the white space. The first unit will be named "_EMPLOYEES" and the second one "_ADMINS".
</p>
<br />

![Screenshot 2025-01-31 202350](https://github.com/user-attachments/assets/53387ce3-f86d-4cce-a6b9-e8520dc343bb)

![Screenshot 2025-01-31 202451](https://github.com/user-attachments/assets/2d9b8801-66aa-47e2-9a04-be2629dde9e4)

![Screenshot 2025-01-31 202552](https://github.com/user-attachments/assets/7dbf2d8c-86db-47c5-a5c7-4f5f46cc76c2)

<p>
After, we will create a new admin user by clicking to top button with a person and star on it. Name the user Jane Doe and the login username to "jane_admin". In the next screen, uncheck "User must cahnge password at next logon" then hit next to create the user.
</p>
<br />

![Screenshot 2025-01-31 202639](https://github.com/user-attachments/assets/708e9ab5-678e-4071-95ec-88d80e523e2b)

![Screenshot 2025-01-31 202808](https://github.com/user-attachments/assets/22ec1b0b-d085-4985-8cac-24d92b1eb197)


<p>
Next, add Jane Doe to the group "Domain Admins". To perfom this step, right click on Jane > Properties > Member Of > Add > type "Domain" in the object box > Check Names > click "Domain Admins" > click Ok and then apply. After this, you will logout and log on to DC-1 as jane_admin.

</p>
<br />


![Screenshot 2025-01-31 203235](https://github.com/user-attachments/assets/6231cef5-b77b-45fb-b677-bb2dfb5192c4)

![Screenshot 2025-01-31 204102](https://github.com/user-attachments/assets/2528bc2a-90ac-4df0-8184-9ed5e1818c11)

![Screenshot 2025-01-31 204342](https://github.com/user-attachments/assets/59eb2f19-9d64-419e-88bd-30574a81410c)

<p>
When inside Client-1, go to Settings > About > Rename this PC(Advanced) > change domain > type mydomain.com > use mydomain.com\jane_admin > then press ok to make the changes apply. Restart Client-1 and log into jane_admin.
</p>
<br />

![Screenshot 2025-01-31 210225](https://github.com/user-attachments/assets/a9d352ad-fc37-488e-8deb-4b91401cf645)

![Screenshot 2025-01-31 211211](https://github.com/user-attachments/assets/1da05365-d974-415e-b7cd-07981e52b3f6)


<p>
After logging in, go to Remote Desktop Settings and click "Select users that can remotely access this PC" > add > type "domain users" in the object box > check names and then hit OK. This will allow all domain users to connect to Client-1.
</p>
<br />

![Screenshot 2025-01-31 204554](https://github.com/user-attachments/assets/99b85c11-d40f-41ea-a0b8-f99d71895a90)

![Screenshot 2025-01-31 204811](https://github.com/user-attachments/assets/4688f916-0c6a-4e70-ac78-1084eeb791cd)


<p>
Head back to DC-1 and into ADUC in the server manager application. Check to see if Client-1 is listed by clicking into mydomain and computers where you should see Client-1.
</p>
<br />


<h1>Stay Tuned for On-premises Active Directory within Azure VMs Part 3</h1>
