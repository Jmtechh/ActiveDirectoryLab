<h1>Active Directory HomeLab</h1>


<h2>Description</h2>
The aim of this lab is to pracitce using Active directory via virtual box. In this lab I create two Windows virtual machines. One of them will be the domain controller which I will install Active Directory and the other will be the client PC that will be under the domain of the domain controller PC. One of the goals of this lab is to enable network communication between the two virtual machines through IP address, routing and NAT. Another goal is to create multiple users and input it into Active Directory under the users folder. This will be done by running a script in powershell that automatically inputs a list of users/names into the AD system.


<h2>Utilities Used</h2>

- <b>Virtualbox</b>
- <b>virtual machines</b>
- <b>Windows ISO</b> 

<h2>Environments Used </h2>

- <b>Windows 10 OS</b>
- <b>Windows 10 server OS</b> 

<h2>Program walk-through:</h2>
The first thing I did was open up Virtualbox and create a Windows virtual machine that was dedicated to be the doimain controller.


<img src="https://i.imgur.com/xmKdgdn.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>   
<br />
After I finished creating the domain controller Windows virtual machine. I then configured two virtual NICs so the domain controller can access networks and communicate with other devices. 
One NIC has a NAT network adapter attatched to it. The NAT allows the network adapter to get IP addressing and internet from the home router network. While the other NIC is dedicated for internal communication through it's attatched network adapter configurations.
<br />
<br />
<img src="https://i.imgur.com/nzvvzZh.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Once I have installed the Windows server operating system ISO onto the virtual machine. The domain controller virtual machine creation is complete.
<br />
<br />
<img src="https://i.imgur.com/18RqNoE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Now that the virtual machine is up and running. I assigned network IP addressing to the internal NIC since it will not be getting it's IP address from the home router network so I must create a static IP address for this internal/private network.
<br />
<br />
<img src="https://i.imgur.com/e5Mho2Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Next I installed Active Directory Domain Services using the server manager that comes with the Windows server ISO. Installing Active Directory Domain Services enables me to set the current virtual machine as a domain that other computers/devices can join.
<br />
<br />
<img src="https://i.imgur.com/xOe6Rom.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
The next service I installed was Remote Access. This service enabled me to configure routing and NAT. The routing will allow the domain controller virtual machine to communicate with other devices on a network.  The NAT feature will allow the clients/PCs on a private network to connect to the internet through the domain controller, since the domain controller will have internet access and NAT installed.

<img src="https://i.imgur.com/TOLwWQ9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


After installing the Remote access service. I installed the DHCP service onto the domain controller virtual machine via the server manager application. The DHCP will help me to automatically provide the client PC with an IP address so that it can communicate with the domain controller virtual machine/PC when I add it to the domain of the domain controller.

From within the DHCP service I configured a scope range. This scope is basically a pool of IP addresses that can be used by computer devices for networking communication. The scope is intened to provide the client PC with an IP address within a specific network/pool. In this setup, the network scope is linked to the domain controller's internal network adapter. This allows the DHCP server to assign an IP address to the client PC, enabling it to communicate with the domain controller through its internal network adapter.
<br />
<br />
<br />
<img src="https://i.imgur.com/Mi77oSM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Another thing that I configured when setting up DHCP was scope options. One of the options is
<br />
<br />
<img src="https://i.imgur.com/KHG9Tp2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
I now have AD DS (Active Directory Domain Services), RAS (Remote Access), DHCP (Dynamic Host Configuration Protocol), and NAT (Network Address Translation) installed onto the Windows domain controller via the server manager application. These services combined allow me to carry out the aim of this lab.
<br />
<br />
<img src="https://i.imgur.com/HY7DVKj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

The next step in the lab is to automatically populate the recently installed Active Directory Service with users. This is done by running a powershell script.

<img src="https://i.imgur.com/4un3gdE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

Now the next part of this lab is to create a new virtual machine that is dedicated to be a client PC under the domain of the domain controller PC.

<img src="https://i.imgur.com/8DKOt8b.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
After creating the virtual machine I attatch an internal NIC/network adapter which enables network communication with the domain controller virtual machine since it also has an internal NIC/network adapter.
<br />
<br />
<img src="https://i.imgur.com/Y6RUWUm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Once I have installed the Windows 10 operating system ISO onto the virtual machine. The creation of client PC is complete. When I go to start up the virtual machine I will be prompted to attatch the Windows ISO which will begin the installation process of the Windows operation system onto to the virtual machine.
<br />
<br />
<img src="https://i.imgur.com/87Fx3MF.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
One thing I verifed once the client PC is running was weather or not the DHCP has provided the client with the correct IP addressing to communicate, network and access the internet.

So I opened up the command prompt and ran "ipconfig" which showed me the networking configurations to this virtual machine... 

As you can see the IPV4 address comes under the DHCP scope that I configured on the domain controller earlier. This means the client device has joined the internal network of the domain controller. The DHCP on the domain controller has also assigned a subnet mask which is ued in combination with the IPV4 address for network identification and communication. And lastly the DHCP has given the client PC a defualt gateway IP address to refer to when it needs to access the internet, access external networks, and resolve external DNS queries.
<br />
<br />

<img src="https://i.imgur.com/Y68Q04z.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
When I go back to Active Directory on the domain controller vm. You can see an IP address under the lease folder. The IP address is the same IP address that you see when you look at the IP address given to the client virtual machine in the image above.
<br />
<br />
This shows that the DHCP server has leased an IP address to the client device which is extra verification that the client is apart of the network of the domain controller.
<br />
<br />

<img src="https://i.imgur.com/OkMwZL1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Another thing that I verify in the in the command terminal is weather or not this new virtual machine can resolve DNS queries and access the internet via the IPV4 IP address and the default gateway. 

At one point the client was not recieving internet but I fixed this issue with the DNS forwarder feature...

Initially, the client VM could communicate with the DC and obtain an IP address via DHCP, but it couldn't access the internet because it was using the DC (172.16.0.1) as its DNS server. The DC’s DNS server was only set up to resolve internal domain names (e.g., your domain corp.local) and didn’t know how to resolve external websites (like google.com).

To fix this, I configured the DC’s DNS server to forward any external DNS queries to my home router's IP address. This allowed the DC to pass on queries it couldn’t resolve internally to the router, which could reach the internet. As a result, the client VM could now resolve external domain names and access the internet through the DC’s NAT and DNS forwarding setup.

And to test that the client Vm could resolve the external domain names and access the internet I ran some ping tests.

I first pinged youtube.com to see if the virtual machine reslove DNS addresses. I next pinged the IP address of youtube.com to see if the deviece can also access the internet.

As you can see they both returned packets which means that everything sould be working as they should.

<img src="https://i.imgur.com/LUbc6Gc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

I then added the client VM to the domain of the Domain Controller VM by going into the settings of the client machine and setting it up.

<img src="https://i.imgur.com/fW2k5Tv.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
As you can see the client VM device has beed added to the Active Directoryunder the computer folder which verifies that the client VM has been added to the domain.
<br />
<br />
<img src="https://i.imgur.com/3mvzlKR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
After I added the client VM to the domain. I logged into one of the users accounts that I created when running the powershell script from earlier.
<br />
<br />
<img src="https://i.imgur.com/ipR7ypL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<img src="https://i.imgur.com/mlqlaYZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
As you can see when I ran the command "whoami" in the cmd terminal, it displayed the new domain next to the users name which verifies that the client is now apart of "mydomain" which is the domain controllers domain name.
<br />
<br />
<img src="https://i.imgur.com/hUWi20G.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>




<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
