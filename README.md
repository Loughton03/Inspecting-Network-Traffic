<p align="center">
<img src="https://i.imgur.com/wrBxEZP.png" alt="osTicket logo"/>
</p>

<h1>Inspecting Network Traffic Between Azure Virtual Machines</h1>
In this lab, I explored and analyzed network traffic to and from Azure virtual machines using Wireshark and experimented with network security groups to better understand their impact on traffic control.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection
- Command-Line Tools
- Network Protocols: SSH, RDP, DNS, HTTP/S, ICMP
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>
- Windows 10</b> (21H2)
- Ubuntu Server 22.04

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket Installation Files

<h2>Lab Set-Up</h2>
<p>I created two virtual machines within Azure on the same virtual network to enable internal communication. One VM was configured with Windows 10 Pro and the other with Ubuntu Server 20.04.</p>

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/42cavvb.png" height="80%" width="80%" alt="Resource Group Setup"/>
</p>

<p>
Using Remote Desktop Connection, I connected to the Windows VM using its public IP address and installed Wireshark to begin traffic inspection.
</p>

<p>
<b>ICMP Traffic Analysis:</b>

<img src="" height="80%" width="80%" alt="place-holder"/>
  
I filtered for ICMP (Internet Control Message Protocol) traffic in Wireshark and used PowerShell to execute the ping command. This command uses ICMP to test connectivity by pinging the Ubuntu VM's private IP and google.com. I then used a continuous ping (ping -t [IP address]) to monitor traffic and demonstrate how network security groups function.

<img src="" height="80%" width="80%" alt="place-holder"/>

In the Azure portal, I added an inbound rule to the Ubuntu VM's network security group to block ICMP traffic, ensuring it had a higher priority than the SSH rule (priority 300) to apply the block first. 

<img src="" height="80%" width="80%" alt="place-holder"/>

Upon returning to the Windows VM, I observed that ICMP traffic was indeed blocked until I lifted the rule; at this point, the continuous ping resumed without timeouts.
</p>
   

<p>
SSH Traffic Analysis:

<img src="" height="80%" width="80%" alt="place-holder"/>
  
Using PowerShell, I connected to the Ubuntu server via SSH and filtered Wireshark traffic for tcp port == 22 to capture SSH sessions. Each command executed on the Ubuntu server was logged in Wireshark, giving visibility into the SSH session traffic.
</p>

<p>
DHCP Traffic Analysis:

<img src="" height="80%" width="80%" alt="place-holder"/>

After logging out of the Ubuntu server, I filtered Wireshark for DHCP traffic. Using the ipconfig /renew command, I requested a new IP address from my VM, causing a brief disconnection as the IP renewed. Wireshark displayed the resulting DHCP traffic, showing the IP assignment process.
</p>

<p>
DNS Traffic Analysis:

<img src="" height="80%" width="80%" alt="place-holder"/>

I filtered Wireshark for DNS traffic on udp port == 53 and used the nslookup command to query google.com and disney.com. The captured traffic displayed the DNS resolution process for these domains.
</p>

<p>
RDP Traffic Analysis:

<img src="" height="80%" width="80%" alt="place-holder"/>

Finally, I observed RDP (Remote Desktop Protocol) traffic using Wireshark's filter tcp port == 3389. Since RDP continuously streams a live feed from one machine to another, there was a constant traffic flow as I accessed the Azure-hosted VM from my local machine.
</p>

<p>
This lab provided valuable insights into how various protocols and ports function within a networked environment. Although it wasn't a troubleshooting exercise, it demonstrated how Wireshark and command-line tools can observe network traffic and understand its flow through different protocols.
</p>
<br />


