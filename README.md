# Configuring an Active Directory Home Lab
<h2>Description</h2>
This is a simple Active Directory home lab. I've set up Windows Server 2019 on VirtualBox to create a Domain Controller that houses Active Directory. The Domain Controller has two network adapters, one that connects my external network, and the other that connects to the clients running Windows 10 on the internal network. Remote Access Services and Network Address Translation are configured so the clients on the internal network can access the internet through the Domain Controller. DHCP is configured to automatically assign IP addresses to clients. A PowerShell script is used automatically create 1,000 users.
<h2>Environments Used </h2>
- <b>Windows Server 2019</b> (17763) </br>
- <b>Windows 10</b> (22H2)
<h2>Utilities Used</h2>
- <b>PowerShell</b>
<h2>Home Lab Diagram</h2> 
<img src="https://i.imgur.com/dpFmLFm.png" height="80%" width="80%" alt="Home Lab Diagram"/>
<br/>
<h2>Active Directory Setup Walkthrough</h2> 
After installing Windows Server 2019, I assigned an IP of 172.16.0.1 and a Subnet mask of 255.255.255.0 to the internal network adapter and used a loopback address for the preferred DNS server.
<img src="https://i.imgur.com/QTJqvTB.png" alt="Internal Network Config"/>
</br>
Installed Active Directory Domain Services and created the domain mydomain.com.
<img src="https://i.imgur.com/RLgjIgs.png" alt="Active Directory Domain Services"/>
</br>
Created an _ADMINS Organizational Unit (OU) and admin account within that OU. I then logged into that admin account.
<img src="https://i.imgur.com/a4yBLrc.png" alt="Admin Account"/>
</br>
Installed Remote Access Services onto the Domain Controller and configured Network Address Translation to allow clients to access the external network through the Domain Controller.
<img src="https://i.imgur.com/tKm0bNg.png" alt="Remote Access Services"/>
<img src="https://i.imgur.com/vJnmc4M.png" alt="Network Address Translation"/>
</br>
Installed a DHCP server to assign IP addresses to the clients. I created a new scope for the addresses 172.16.0.100-200, and then set the internal NIC as the Default Gateway for the clients and configured the domain to be used as the DNS server.
<img src="https://i.imgur.com/GCncdPS.png" alt="DHCP"/>
<img src="https://i.imgur.com/6j4D22A.png" alt="Scope"/>
<img src="https://i.imgur.com/Me7iKpo.png" alt="Default Gateway"/>
</br>
In PowerShell, I set ExecutionPolicy to Unrestricted to allow the user creation script to run. I ran the script, which created a new _USERS OU and generated ~1,000 users based on a list of randomly generated names.
<img src="https://i.imgur.com/ruvQIQE.png" alt="Users PowerShell Script"/>
</br>
I configured the client VM, and after setting up Windows 10 and logging in, the client was connected to the Domain Controller. The DHCP server assigned it an IP address of 172.16.0.100. I'm able to ping www.google.com from the client to confirm its connection to the external network as well as the DNS are working properly
<img src="https://i.imgur.com/ZFomt5H.png" alt="Client ipconfig"/>
<img src="https://i.imgur.com/QPxPl4V.png" alt="Ping test"/>
</br>
The client is renamed to CLIENT1 and mydomain.com is joined. After that, I check in with the DHCP server on the Domain Controller to confirm that 172.16.0.100 has been leased to CLIENT1. Since CLIENT1 has been joined with mydomain.com, it also appears under Computers in Active Directory Users and Computers. This allows any of the users created to log into the CLIENT1.
<img src="https://i.imgur.com/rWjijA5.png" alt="Joining mydomain.com"/>
<img src="https://i.imgur.com/wGa6H44.png" alt="DHCP Lease"/>
<img src="https://i.imgur.com/hshmeJ0.png" alt="CLIENT1"/>
</br>
I used one of the generated users to sign into the mydomain.com using CLIENT1. I then opened command prompt and typed whoami to confirm that I am actually connected to mydomain.com.
<img src="https://imgur.com/vT0d7mu.gif" alt="CLIENT1 Sign In"/>
</br>
