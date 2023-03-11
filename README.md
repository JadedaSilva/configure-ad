<p align="center">
  <img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo" />
</p>
<h1>On-Premises Active Directory Deployed in the Cloud (Azure)</h1>
<p>This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.</p>
<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Active Directory Domain Services</li>
  <li>PowerShell</li>
</ul>
<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 (21H2)</li>
</ul>
<h2>High-Level Deployment and Configuration Steps</h2>
<ol>
  <li>Step 1</li>
  <li>Step 2</li>
  <li>Step 3</li>
  <li>Step 4</li>
</ol>
<h2>Deployment and Configuration Steps</h2>
<h3>Setup a Domain Controller (Windows Server) and Test Machine (Windows 10)</h3>
<p>
  <img src="https://i.imgur.com/ubZebIP.png" height="80%" width="80%" alt="DC and Test Machine Setup" />
</p>
<h3>Setting the DC IP to Static IP</h3>
<p>Go to the DC you created and click on Networking, then click on the NIC. Go to IP configurations, click on the IP address, select "Static," and save.</p>
<p>
  <img src="https://i.imgur.com/qHVuVG0.png" height="80%" width="80%" alt="Setting DC IP to Static IP" /><br /><br />
  <img src="https://i.imgur.com/Wz0pDkJ.png" height="80%" width="80%" alt="Setting DC IP to Static IP" /><br /><br />
  <img src="https://i.imgur.com/IZXocPK.png" height="80%" width="80%" alt="Setting DC IP to Static IP" />
</p>
<h3>Add Inbound Rules for ICMP Traffic Allow on Local Subnet</h3>
<p>In the search bar, type "wf.msc" and hit Enter. Then, go to Core Networking Diagnostics, click on ICMP (v4/v6 local subnet), right-click, and select "Enable Rule."</p>
<p>
  <img src="https://i.imgur.com/Txd6tpX.png" height="80%" width="80%" alt="Adding Inbound Rules for ICMP Traffic" />
</p>
<p>
  <img src="https://i.imgur.com/lqrKZDl.png" height="80%" width="80%" alt="Adding Inbound Rules for ICMP Traffic" />
</p>
<h3>Ping the DC from the Windows 10 Client</h3>
<p>Go to CMD and ping the DC from the Windows 10 client by entering "ping 10.0.0.4." You should receive a reply from the DC.</p>
<p>
  <img src="https://i.imgur.com/RrrxYAM.png" height="80%" width="80%" alt="Pinging DC from Windows 10 Client" />
</p>
<h3>Active Directory Install</h3>
<p>Go to Server Manager (ServerManager.msc), click on "Manage," then go to "Add Roles and Features." Keep clicking "Next" and install "



Jade da Silva
carry on
<h3>Join Windows 10 client to the Domain</h3>
<p>
Go to Windows 10 client, click on start button, and type "System" in the search bar, and click on the "System" settings. Then click on "Change Settings". Click on "Change" then select the radio button next to "Domain" and type the name of the domain you have created. In this case, it is "thisdomain.local". Click on "OK" and enter the domain credentials to join the Windows 10 machine to the domain.
</p>
<br />
<p>
<img src="https://i.imgur.com/ehfLg22.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<h3>Verify Windows 10 client is joined to the Domain</h3>
<p>
Restart the Windows 10 machine and log in with the domain credentials. After logging in, go to "System" settings again, and under "About", check if the Windows 10 machine is joined to the domain.
</p>
<br />
<p>
<img src="https://i.imgur.com/BX9SYOZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h2>Conclusion</h2>
In conclusion, this tutorial has outlined the implementation of on-premises Active Directory within Azure Virtual Machines. The process involves setting up a Domain Controller and Windows 10 client machine, configuring DNS, adding inbound rules for ICMP traffic, and joining the client machine to the domain. By following these steps, users can easily deploy on-premises Active Directory in the cloud with Azure Virtual Machines.
