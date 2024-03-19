# Active Directory Home Lab

<h2>Description</h2>

This is a simple Active Directory home lab. I've set up Windows Server 2019 on VirtualBox to create a Domain Controller that houses Active Directory. The Domain Controller has two network adapters, one that connects my external network, and the other that connects to the clients running Windows 10 on the internal network. Remote Access Services and Network Address Translation are configured so the clients on the internal network can access the internet through the Domain Controller. DHCP is configured to automatically assign IP addresses to clients. A PowerShell script is used automatically create 1,000 users.

<h2>Environments Used </h2>

- <b>Windows Server 2019</b> (17763)
- <b>Windows 10</b> (22H2)

<h2>Utilities Used</h2>

- <b>PowerShell</b>

<h2>Home Lab Diagram</h2> 
<img src="https://i.imgur.com/dpFmLFm.png" height="80%" width="80%" alt="Home Lab Diagram"/>
<br/>
<h2>Active Directory Setup Walkthrough</h2> 
