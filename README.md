<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Creating a Active Direcotry Enviornment in Azure </h1>
This tutorial outlines the implementation of creating a Virtual Network and Virtual Machines in Azure. I will be creating a setup for a one server and client Active Directory Lab.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Domain Name Services
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup a Resource group and Virtual Network
- create 2 virtual machines in Azure
- configure DNS on the client to point to the server
- install Active Directory and create a domain

<h2>Setting up Azure Environment </h2>
<p> For this section we will do the following

<ul>
  <li>Create a resource group</li>
  <li>Create a Virtual Network</li>
  <li>Create 2 Virtual Machines </li>
<li> Create a Domain Controller</li>
<li>Join a windows 10 client to the domain </li>
</ul> </p>

<p> This image is what is shown when you log into azure </p>

<img src="https://i.imgur.com/lGqROTH.png" alt="AzureScreen"/>

<p> The first thing we are going to do is create a resource group, you can do this while creating the VM but I will demonstrate how to do it manually. Click on Resource Groups, if it is not there using the search bar at the top of the screen. Click on create in the upper left corner of the screen. On the next screen we are going to name our resource group “ADDS_Lab” which stands for Active Directory Domain Services. For the region I will be selecting West US 2. You can proceed by selecting Review and Create, then Create. You will be taken back to the resource group page; you may need to refresh in order to see it. You will also have a notification in the upper right corner saying “Resource Group Created” </p>

<img src="https://i.imgur.com/DOYfWyl.png" alt="Create a RG1"/>
<img src="https://i.imgur.com/kHFTxsB.png" alt="Create a RG 2"/>
<img src="https://i.imgur.com/ODYTboY.png" alt="Create a RG 3"/>


<p> Now we are going to create a Virtual Network, this will allow our VM’s to talk to each other, again this can be done while creating the virtual machines but I will show you how to do it manually. on the home page, select Virtual Networks or type it in the search at the top. </p>

<p> On the Create virtual network screen be sure the ADDS_Lab resource group is selected, we are going to name this Virtual Network “ADVNET”, again we are sticking with West US2 as the region. I am not going to mess with the settings on the following screen so I will select review and create, then create. you will get to a screen that says “your deployment is complete” </p>
<img src="https://i.imgur.com/EJe3KVN.png" alt="VNET1"/>
<img src="https://i.imgur.com/kcWxXX4.png" alt="VNET2"/>
<img src="https://i.imgur.com/yTOYTWK.png" alt="VNET3"/>


<p> Now we are going to create our virtual machines. On the home page select Virtual Machines then select create, a drop-down menu will come up. Select “Azure Virtual Machine” </p>
<p> On the next screen use the drop-down menu on resource group to ADDS_Lab. Name the VM DC-1, we are going to select the region as “West US 2”.  For the image select windows server 2022. I have had an issue where I cannot select the size of the virtual machine and get an error. To get around this I select “Azure selected zone (preview) and I can select s size. I am going to do at least 2 vcpus. While doing the labs for Course Careers I made the mistake of selecting 1 vcpu and that was very slow. Be sure to only select 2 if you are on the trial plan as you have a limit of 4 vcpus. I made the error of selecting 4 while setting this up and had to repeat the process. For the username and password I am going to have a username of LabUSER and a password of CyberLab1234. Select Next, then Next again to get to network. </p>
<p> On the Networking tab make sure the virtual network is set to ADVNET. Click on review and create. If validation passes go ahead and click create. This may take some time but once your screen gets to deployment in process repeat the process except select windows 10 and name it “Client-1”. Be sure to keep it on the same resource group and virtual network. The windows 10 VM will require you to confirm licensing. Be sure to check this box at the bottom or the validation will fail. </p>

<p> Now that both VM’s are created we are going to do a few things., first we are going to get the public IP address of both VMs. This is found under virtual machines, and displayed with the VM These will be used in remote desktop to connect to the VM 
 <ul>
  <li>Server – 20.9.133.119 </li>
  <li>Client – 52.233.82.250</li> </ul> </p>

<img src="https://i.imgur.com/p8epYNP.png" alt="CreateVM"/>
<img src="https://i.imgur.com/I2NHQf7.png" alt="CreateVM"/>
<img src="https://i.imgur.com/Tweb3rn.png" alt="CreateVM"/>
<img src="https://i.imgur.com/6bAEJbl.png" alt="CreateVM"/>
<img src="https://i.imgur.com/DLyBOA0.png" alt="CreateVM"/>
<img src="https://i.imgur.com/lHwU8vv.png" alt="CreateVM"/>
<img src="https://i.imgur.com/2jaQFuA.png" alt="CreateVM"/>
<img src="https://i.imgur.com/dI4ZxGD.png" alt="CreateVM"/>

<p> Now on windows go to the start menu by selecting the start button or hitting the windows key, type RDP. RDP stands for “remote desktop protocol” you can also type remote desktop but I find this faster.   you will need to type in the IP address we collected before then log in as different user, then log in with the credentials you created before. Let the two virtual machines log in. this will take time as it’s the first install. On the windows 10 VM go through the install process </p>

<img src="https://i.imgur.com/0bhyecL.png" alt="EDP"/>
<img src="https://i.imgur.com/VX2hh13.png" alt="RDP"/>
<img src="https://i.imgur.com/5dEZF90.png" alt="RDP"/>

<p> Now we are going into the windows server VM.  Go to the command prompt or PowerShell by searching CMD or PowerShell on the start menu. Type ipconfig and find the local IP address. This is under IPV4. We have an IP address of 10.0.0.5. now go into azure. And select Client1 under virtual machines. On the side panel expand networking and select network settings. Click on network interface / IP address. on the side panel you will see DNS servers under settings. Select this and select custom. add the IP address of the DC-1. This is so the client will look to the server for DNS, which is required for the domain, once that is done click save. restart the VM by going to virtual machines page select Client1. Confirm yes to restart the VM, your remote desktop session should be kicked off. That is normal. We only went in to get the lengthy setup complete. When it is complete log back into the VM and go to PowerShell. Type ipconfig /all to verify the DNS is pointing to the server. We are all done setting up azure. The next section will go over how to setup a domain controller </p>
<img src="https://i.imgur.com/dYcMVKh.png" alt="DNS"/>
<img src="https://i.imgur.com/5mkyE7y.png" alt="DNS"/>
<img src="https://i.imgur.com/9IMk7e8.png" alt="DNS"/>
<img src="https://i.imgur.com/aiEdDTM.png" alt="DNS"/>
<img src="https://i.imgur.com/2PTZSR0.png" alt="DNS"/>
<img src="https://i.imgur.com/LhFMOBp.png" alt="DNS"/>






<h2>Installing Active Directory Domain Services </h2>

<p> The first thing we are going to do is install active directory domain services. Open the DC-1 VM server manager should open automatically. If not open it now. On the welcome screen, click add roles and features. when the menu opens click next 3 times, we don’t need to do anything there. Select “Active Directory Domain Services. This will open a window asking you if you also want to install some prerequisites. Click add features. This will install everything needed for Active Directory. click next 3 more times, then click install. This may take some time but you can close the wizard. Once completed there will be an alert icon in the top right corner of server manager. click it then select “Promote this server to a domain controller” select add a new forest and name your domain. I will be going with mydomain.com as this is a test environment. Click next on the domain controller options we are going to leave everything alone except add a password. The password here is P@ssw0rd1. Do not use weak passwords in a real environment. Click next. We aren’t going to create a DNS delegation so click next again until you get to Prerequisites check if everything looks good go ahead and click install.  The domain will be created and the server will restart automatically </p>

<img src="https://i.imgur.com/g0Bhzbi.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/fohAjLR.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/fj1BHOF.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/gJpDGG2.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/DLoSlEw.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/9euZMfJ.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/EHY4diF.png" alt="INSTALL ADDC"/>
<img src="https://i.imgur.com/ZWDv65T.png" alt="INSTALL ADDC"/>


<p> When you go back into the VM it will take some time to setup the domain.  Next, we are going to create 2 Organizational units called _EMPLOYEES and _ADMIN. In server manager go to tools and click on “Active Directory Users and computers. Expand your domain then right Click and create a new OU. Name it _EMPLOYEES and click OK repeat this process with _ADMIN. now we are going to create a domain admin name Jane Doe. To do this right click on _ADMIN and select New then user. On the next screen we are going to fill out the information about the user click next and give the user a password. Because this is a testing environment the password will be P@ssw0rd1. Click next then finish. We are not going to right click the user and select properties. Click members of at the top. Click add, the on the next box type in Domain admins in the “enter the object names to select”, click check names. If its underlined it worked. click ok. I am going to create one user under _EMPLOYEES following the same process under the name of john.doe. </p>
<img src="https://i.imgur.com/GQxFUfy.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/9sLXcvY.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/YrOc3GJ.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/5ScBurU.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/sZKBslF.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/yV705aO.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/I2lSsnL.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/9k17r8J.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/GV0kHtf.png" alt="Create OU and Users"/>
<img src="https://i.imgur.com/gzhSG1d.png" alt="Create OU and Users"/>


<h2> Joining a Windows 10 Client to a domain </h2>

 <p>Now we are going to join our client to the domain.  Log into client1 go to the control panel, navigate to system and security and click system. Click rename this PC click change on domain/workgroup and enter domain details then log in with admin account when you get a message saying welcome to the domain restart the computer. The computer is now on the domain </p>
<img src="https://i.imgur.com/mwZxPVe.png" alt="Join Domain"/>
<img src="https://i.imgur.com/3nK2VdF.png" alt="Join Domain"/>
<img src="https://i.imgur.com/qZQn59I.png" alt="Join Domain"/>
<img src="https://i.imgur.com/v6agFht.png" alt="Join Domain"/>
<img src="https://i.imgur.com/F4LM2AH.png" alt="Join Domain"/>
<img src="https://i.imgur.com/BXKH1hB.png" alt="Join Domain"/>
<img src="https://i.imgur.com/TgCCy6B.png" alt="Join Domain"/>
<img src="https://i.imgur.com/GRs2f9J.png" alt="Join Domain"/>


