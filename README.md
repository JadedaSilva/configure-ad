<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>
<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />
<h2>Environments and Technologies Used</h2>
Microsoft Azure (Virtual Machines/Compute)
Remote Desktop
Active Directory Domain Services
PowerShell
<h2>Operating Systems Used</h2>
Windows Server 2022
Windows 10 (21H2)
<h2>High-Level Deployment and Configuration Steps</h2>
Step 1
Step 2
Step 3
Step 4
<h2>Deployment and Configuration Steps</h2>
<p>
<h3>Setup a Domain Controller (Windows server) and Test machine (Windows 10)</h3>
</p>
<p>
<img src="https://i.imgur.com/ubZebIP.png" height="80%" width="80%"/>
</p>
<br />
<h3>Setting the DC IP to Static IP.</h3> 
<p>
Go to the DC you created and click on Networking and then click on the NIC. Then go to IP configurations then click on the IP config. Select static and save.
</p>
<p>
<img src="https://i.imgur.com/qHVuVG0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br><br/>
<img src="https://i.imgur.com/Wz0pDkJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br><br/>
<img src="https://i.imgur.com/IZXocPK.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>  
</p>
<br />
<h3>Add inbound rules for ICMP traffic allow on local subnet</h3> 
<p>
In the search bar type wf.msc, hit enter. Then go to core networking diagnostics - ICMP (v4/v6 local subnet) right click and select enable rule.
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
Go to CMD and ping the DC from the Windows 10 client in this case "ping 10.0.0.4". You should receive a reply from the DC. 
</p>
<br />
<br />
<p>
<img src="https://i.imgur.com/RrrxYAM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<h3>Active Directory Install</h3> 
<p>
Go to server manager (ServerManager.msc) click on "Manage" then go to "Add Roles and Features" keep clicking next and install "Active Directory Domain Services". It should restart after the install.
</p>
<br />
<br />
<p>
<img src="https://i.imgur.com/YB0uwlQ.png" height="80%" width="80%" alt="AD Setup"/>
</p>
<h3>Promote Server to Domain Controller</h3> 
<p>
Click on the flag at the top right-hand corner then click on "Promote this server to a DC". Click "



Jade da Silva
go on
<h3>Adding Devices to the Domain</h3> 
<p>
Right click on device-1 > Properties > Change > Domain > enter the domain name you created. Then enter the credentials of a domain admin account that you created earlier. Restart after it's completed.
</p>
<br />
<p>
<img src="https://i.imgur.com/ie7DMVS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<h3>Verify Domain Account Access</h3> 
<p>
Login with the user you had created in the domain admin account. Then create a new account on the Windows 10 machine. Try and log in with the account you had created on the Windows 10 machine. You will receive a message saying that you can't log in. This is because you haven't given the user access to the device yet. To do that go to the DC > dsa.msc > device-1>properties>security>add user account>advanced. Find the user account then click on "Check Names". Click on "OK". You can now log in with the account you created earlier.
</p>
<br />
<p>
<img src="https://i.imgur.com/QKjOxI5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
<img src="https://i.imgur.com/09E6bAz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
<img src="https://i.imgur.com/ZQ1MZyF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
<img src="https://i.imgur.com/TTuozpP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<h3>Assigning Policies to Domain Accounts</h3> 
<p>
Go to Group Policy Management(gpmc.msc). Create a new policy called "Lockout". Click on the policy you just created then click on "Edit". Expand Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy. Right click on "Account Lockout Threshold" then click on properties. Then click on "Define this policy setting" and set it to 3. Click on "OK". The policy should now be applied.
</p>
<br />
<p>
<img src="https://i.imgur.com/tN55tHj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
<img src="https://i.imgur.com/YG4iBl9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
<img src="https://i.imgur.com/3RXqX34.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<h3>Assigning Policies to Specific Devices</h3> 
<p>
Go to dsa.msc > Device-1 > Properties > Group Policy > Edit. Now it's time to create a new policy called "ScreenLock". Expand Policies > Administrative Templates > Control Panel > Personalization. Right click on "Password protect the screen saver" then click on properties. Click on "Define this policy setting" and set it to "Enabled". Click on "OK". Close the policy editor and refresh the Group Policy Management Console. Close dsa.msc.
</p>
<br />
<p>
<img src="https://i.imgur.com/N12ebft.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<b/>
