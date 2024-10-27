<h1>Active Directory HomeLab</h1>


<h2>Description</h2>
The aim of this lab is to pracitce using Active directory via virtual box. In this lab I create two Windows virtual machines. One of them will be the domain controller which I will install Active Directory and the other will be the client PC that will be under the domain of the domain controller. This lab will include networking, user creation in AD, IP addressing, routing, NAT, domain controll, and scripting. 


<h2>Utilities Used</h2>

- <b>Virtualbox</b>
- <b>Windows virtual machines</b> 

<h2>Environments Used </h2>

- <b>Windows 10</b> 

<h2>Program walk-through:</h2>
The first thing I did was open up Virtualbox and create a Windows virtual machine that was dedicated to be the doimain controller.


<img src="https://i.imgur.com/xmKdgdn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>   
<br />
<br />
After I finished creating the domain controller Windows virtual machine. I then configured two virtual NICs so the domain controller can access networks and communicate with other devices. 
One NIC has a NAT network adapter attatched to it. The NAT allows the network adapter to get IP addressing and internet from the home router network. While the other NIC is dedicated for internal communication through it's attatched network adapter configurations.
<br />
<br />
<img src="https://i.imgur.com/nzvvzZh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

Once I have installed the Windows server operating system ISO. The domain controller virtual machine creation is complete.
<br />
<br />
<img src="https://i.imgur.com/18RqNoE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Now that the virtual machine is up and running. I need to assign network IP addressing to the internal NIC since it will not be getting it's IP address from the home router network so I must create a static IP address for this internal/private network.
<br />
<br />
<img src="https://i.imgur.com/e5Mho2Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
