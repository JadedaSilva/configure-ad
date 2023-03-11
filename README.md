<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>
<p>
<h3>Setup a Domain Controller(Windows server) and Test machine(Windows 10)</h3>
</p>
<p>
<img src="https://i.imgur.com/ubZebIP.png" height="80%" width="80%"/>
</p>

<br />
<h3>Setting the DC Ip to Static Ip.</h3> 
<p>
Go to the DC you created and click on Networking and then click on the NIC. Then got to Ip configurations then click on the ipconfig. Select static and save.
</p>
<p>
<img src="https://i.imgur.com/qHVuVG0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br><br/>
<img src="https://i.imgur.com/Wz0pDkJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br><br/>
<img src="https://i.imgur.com/IZXocPK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
</p>

<br />

<h3>Add inbound rules for icmp traffic allow on local subnet</h3> 
<p>
In the seearch bar type wf.msc, hit enter. Then go to core networking diagnostics - ICMP (v4/v6 local subnet) right click and select enable rule.
</p>
<p>

<p>
<img src="https://i.imgur.com/Txd6tpX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<br />

<p>
<img src="https://i.imgur.com/lqrKZDl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Ping the DC from the Windows 10 Client</h3> 
<p>
Go to CMD and ping the DC from the Windows 10 client in this case "ping 10.0.0.4". you receive a reply from the DC. 
</p>
<br />

<br />

<p>
<img src="https://i.imgur.com/RrrxYAM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<h3>Active Directory Install</h3> 

<p>
Go to server manager (ServerManager.msc) click on "Manage" then go to "Add Roles and Features" keep clicking next and install  "Active Directory Domain Services". It should restart after the install
</p>
<br />

<br />

<p>
<img src="https://i.imgur.com/YB0uwlQ.png" height="80%" width="80%" alt="AD Setup"/>
</p>

<h3>Promote Server to Domain Controller</h3> 
<p>
Click on the Flag at the top right hand corner then click on "Promote this server to a DC". Click "Add a new Forest" then create a domain name. 
</p>
<p>
<img src="https://i.imgur.com/pM7pb0U.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
<img src="https://i.imgur.com/uHOrNzf.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Login with domain name</h3> 

<p>
Now that the domain has been created the can login with "thisdomain\rootuser" in this case.
</p>

<br />

<br />

<p>
<img src="https://i.imgur.com/mZ9pGQk.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Create OUs</h3> 

<p>
Got to Active Directory(dsa.msc), create admin and employee. I had used _ADMIN as it would filter to the top and makes things easier to work with. If not created create a Active account in the admin folder and go to properties and add the user in this domain to "Domain Admins". 
</p>

<br />

<br />

<p>
<img src="https://i.imgur.com/wPbWcgG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/m9rJjDt.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Assigning DNS</h3> 

<p>
Go back to Azure Virtual Machine Device-1(Windows Client) > Networking > NIC(Device-1597) > DNS Servers. Enter you Domain Controllers IP here.
</p>

<br />

<p>
<img src="https://i.imgur.com/lbgTFnM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Adding Device-1(Window 10 Client) to the domain</h3> 

<p>
Login back to the Windows Device-1 right on start go to System > Rename this PC > Change > Domain . Enter the domain name(Thisdomain.com) there.
</p>

<br />

<p>
<img src="https://i.imgur.com/6PcF09O.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/yvvBsFP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<br />

<h3>Allow Remote Access</h3> 

<p>
Select Start  > Settings  > System > Remote Desktop, and turn on Enable Remote Desktop. Select users that can remotely access this PC.
</p>

<br />

<p>
<img src="https://i.imgur.com/vspKXvp.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
