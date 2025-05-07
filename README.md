<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Creating a Virtual Network in Microsoft Azure </h1>
This tutorial outlines the implementation of creating a Virtual Network and Virtual Machines in Azure. I will be creating a setup for a one server and client Active Directory Lab.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup a Resource group and Virtual Network
- create 2 virtual machines in Azure
- configure DNS on the client to point to the server
- install Active Directory and create a domain

<h2>Setting up Azure Environment </h2>

<p>
The first thing we are going to do is create a resource group, you can do this while creating the VM but I will demonstrate how to do it manually. Click on Resource Groups, if it is not there use the search bar at the top of the screen. Click on create in the upper left corner of the screen. On the next screen we are going to name our resource group “ADDS_Lab” which stands for Active Directory Domain Services. For the region I will be selecting West US 2. You can proceed by selecting Review and Create, then Create. You will be taken back to the resource group page, you may need to refresh in order to see it. You will also have a notification in the upper right corner saying “ Resource Group Created”
</p>




<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
 
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="No Alt yet "/>
</p>



<p> For this section we will do the following 
</p>
<ul>
  <li>Create a resource group called “ADDS_Lab</li>
  <li>Create a Virtual Network called “ADVNET</li>
  <li>Create a virtual machine with windows server called “DC-1”</li>
<li> Create a virtual Machine with Windows 10 called “Client1”
</ul>

<p> This image is what is shown when you log into azure </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<p> The first thing we're going to do is create a resource group. You can do this while creating the VM, but I will demonstrate how to do it manually.

Click on Resource Groups. If you don't see it, use the search bar at the top of the screen. Click on Create in the upper-left corner of the screen.

On the next screen, name your resource group "ADDS_Lab", which stands for Active Directory Domain Services. For the region, I will be selecting West US 2.

Proceed by selecting Review + Create, then click Create. You will be taken back to the Resource Groups page—you may need to refresh to see it. A notification will also appear in the upper-right corner saying "Resource Group Created. </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<p> Now we are going to create a Virtual Network. This will allow our VMs to communicate with each other. Again, this can be done while creating the virtual machines, but I will show you how to do it manually. </p>
<p> From the home page, select Virtual Networks, or type it into the search bar at the top. </p>
 <p> On the Create virtual network screen, make sure the ADDS_Lab resource group is selected. We are going to name this virtual network "ADVNET". Once again, we'll stick with West US 2 as the region. </p>
<p> I’m not going to modify the settings on the following screens, so I will select Review + Create, then click Create. </p>

<p> You’ll be taken to a screen that says "Your deployment is complete." </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
 
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<p> Now we are going to create our virtual machines. </p>
<p> From the home page, select Virtual Machines, then click Create. A drop-down menu will appear—select “Azure Virtual Machine.” </p>
<p> On the next screen, use the drop-down menu to select the ADDS_Lab resource group. Name the VM DC-1, and set the region to “West US 2.”
For the image, select Windows Server 2022. </p>
<p> 🔧 Note: I’ve experienced an issue where I couldn't select the VM size and received an error. To work around this, I selected “Azure selected zone (preview),” which then allowed me to choose a size. </p>
<p> Make sure to select at least 2 vCPUs. While doing the labs for CourseCareers, I made the mistake of selecting only 1 vCPU, and performance was very slow.
⚠️ Important: If you're on the Azure trial plan, you have a limit of 4 vCPUs total. Only select 2 vCPUs to avoid hitting that cap. I mistakenly selected 4 the first time and had to start over.
For the credentials: </p>
<ul>
  <li>Username: LabUSER</li>
  <li>Password:CyberLab1234</li>
</ul>
<p> Click Next, then Next again to proceed to the Networking tab.
On the Networking tab, make sure the virtual network is set to ADVNET.
Click Review + Create, and if validation passes, click Create.
⏳ This process may take a few minutes. </p>
 <p>Once you reach the “Deployment in progress” screen, repeat the process to create a second VM. This time:
•	Name it: Client-1
•	Image: Select Windows 10
•	Keep it in the same resource group and virtual network
⚠️ On the Windows 10 VM setup screen, you will need to confirm licensing. Make sure to check the box at the bottom, or the validation will fail. </p>
<p> Now that both VMs are created, we’ll do a few more things. First, we’ll get the public IP addresses of both VMs. You can find these under Virtual Machines, where they are listed next to each VM. These IP addresses will be used for Remote Desktop connections. </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>


<h2>Configuring DNS </h2>
<p> Now, on your client machine, open the Start menu by clicking the Start button or pressing the Windows key on your keyboard. Type "RDP", which stands for Remote Desktop Protocol. (You can also type "Remote Desktop," but I find "RDP" quicker.) </p>
<p> Open the Remote Desktop Connection app. </p>
<p> Next, enter the IP address of the VM you want to connect to—the one we collected earlier. </p>
<p>Click "More choices" or "Use a different account" and log in using the credentials you created earlier: </p>
•	Username: LabUSER
•	Password: CyberLab1234
<p> Let the two virtual machines finish logging in. This may take some time, especially since it’s the first time they're being set up. </p>
<p> Once connected to the Windows 10 VM, go through the standard Windows setup process as prompted. </p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<p> Now we are going into the Windows Server VM. Open the Command Prompt or PowerShell by searching for “CMD” or “PowerShell” in the Start menu. Type ipconfig and find the local IP address listed under IPv4. In this case, the IP address is 10.0.0.5. Next, go into Azure and select “Client1” under Virtual Machines. In the side panel, expand “Networking” and select “Network Settings.” Click on “Network Interface / IP Configuration.” In the side panel that appears, look under “Settings” and select “DNS Servers.” Choose “Custom” and add the IP address of the DC-1 server. This step is necessary so the client machine will look to the server for DNS, which is required for joining a domain. Once that is done, click Save. Then restart the VM by going to the Virtual Machines page, selecting Client1, and confirming “Yes” to restart. Your Remote Desktop session will be disconnected, which is normal. We only accessed the VM initially to complete the lengthy setup process. Once the restart is complete, log back into the VM and open PowerShell. Type ipconfig /all to verify that the DNS is now pointing to the server. </p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<h2>Installing Active Directory and creating a domain </h2>

<p> The first thing we are going to do is install Active Directory Domain Services. </p>

<p> Open the DC-1 VM. Server Manager should open automatically. If not, open it now. </p>

<p> On the welcome screen, click Add Roles and Features. </p>

<p> When the menu opens, click Next 3 times — we don’t need to do anything there. </p>

<p> Select “Active Directory Domain Services.” This will open a window asking if you also want to install some prerequisites. Click Add Features. This will install everything needed for Active Directory. </p>

<p> Click Next 3 more times, then click Install. This may take some time, but you can close the wizard. </p>

<p> Once completed, there will be an alert icon in the top-right corner of Server Manager. Click it, then select “Promote this server to a domain controller.” </p>

<p> Select “Add a new forest” and name your domain. I will be going with mydomain.com as this is a test environment. </p>

<p> Click Next. On the Domain Controller Options page, we are going to leave everything alone except add a password. The password here is P@ssw0rd1.
Do not use weak passwords in a real environment. </p>

<p> Click Next. We aren’t going to create a DNS delegation, so click Next again until you get to Prerequisites Check. </p>

<p> If everything looks good, go ahead and click Install. The domain will be created and the server will restart automatically </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<h2>Creating Organizational Units (OU) and Users</h2>

<p>When you go back into the VM, it will take some time to set up the domain. </p>

<p>Next, we are going to create 2 Organizational Units called _EMPLOYEES and _ADMIN.</p>

<p>In Server Manager, go to Tools and click on “Active Directory Users and Computers.” </p>

<p>Expand your domain, then right-click and create a new OU. Name it _EMPLOYEES and click OK. </p>
<p>Repeat this process for _ADMIN.</p>

<p>Now we are going to create a domain admin named Jane Doe. </p>

<p>To do this, right-click on _ADMIN and select New > User. </p>

<p>On the next screen, we are going to fill out the user information. Click Next and give the user a password.
Because this is a testing environment, the password will be P@ssw0rd1. </p>

<p>Click Next, then Finish. </p>

<p>We are now going to right-click the user and select Properties. </p>
<p>Click on the Member Of tab at the top. </p>

<p>Click Add, then in the next box type Domain Admins in the “Enter the object names to select” field. </p>

<p> Click Check Names — if it's underlined, it worked. Click OK. </p>

<p> I am going to create one user under _EMPLOYEES following the same process, using the name john.doe. </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>

<h2> Joining Our Client to the domain </h2>

<p> Now we are going to join our client to the domain. </p>

<p>Log into Client1. </p>

<p>Go to the Control Panel, navigate to System and Security, and click System. </p>

<p>Click Rename this PC, then click Change under Domain/Workgroup settings. </p>

<p>Enter your domain details, then log in with your admin account. </p>

<p>When you get a message saying "Welcome to the domain", restart the computer. </p>

<p> The computer is now on the domain. </p>

<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Azure Screen "/>
<br />
