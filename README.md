# azure-network-protocols

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we’ll dive into analyzing different network traffic patterns to and from Azure Virtual Machines using Wireshark. Along the way, we’ll also take a closer look at how Network Security Groups work and how they impact network communication.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows and Linux Command Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 22.04

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/EwX8Y7s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.imgur.com/JGhlxJJ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set up two virtual machines in the Azure portal: one with a Windows 10 Pro image and the other with a Linux image, both configured with 2 vCPUs. Make sure to connect both VMs to the same virtual network during the creation process. Once the Windows VM is up and running, use Remote Desktop Protocol (RDP) to connect to it.
</p>
<br />

<p>
<img src="https://i.imgur.com/1BYvdJZ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Head over to https://www.wireshark.org to download and install Wireshark. This powerful tool will help you monitor and analyze network traffic, giving you valuable insights into how data moves across your network.
</p>
<br />

<p>
<img src="https://i.imgur.com/3gTUIDW.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Once you've installed Wireshark, launch the application and use the search bar to filter for ICMP traffic. ICMP, or Internet Control Message Protocol, is a key tool that network devices use to communicate error messages and verify connectivity between devices.
</p>
<br />

<p>
<img src="https://i.imgur.com/HgLp5AR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Open PowerShell and run the ping command to check if you can connect to the Linux machine's private IP address, which is part of the same network. To locate the Linux machine's private IP address, head over to the Azure portal and navigate to the VM's network settings.
</p>
<br />

<p>
<img src="https://i.imgur.com/nurPwTN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
In Wireshark, you can observe every packet transmitted during the ping process, allowing you to analyze the ICMP traffic in detail. 
</p>
<br />

<p>
<img src="https://i.imgur.com/X4yfgee.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, run the ping -t command to continuously send ping requests to the Linux machine. After that, log into the Linux virtual machine on Azure, head over to the Network Settings, and set up an inbound port rule to block ICMP traffic. This will prevent ICMP packets from passing through the firewall.
</p>
<br />

<p>
<img src="https://i.imgur.com/UvdXvva.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
After configuring the Linux machine’s firewall to block ICMP traffic, use Wireshark to confirm that the ping requests no longer receive responses. In PowerShell, you’ll notice a "Request Timed Out" message, indicating that the ICMP packets are being successfully blocked by the firewall.
</p>
<br />

<p>
<img src="https://i.imgur.com/QstVuqS.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, remove the inbound port rule that was allowing ICMP traffic. To end the ongoing ping process, simply press Ctrl + C in the PowerShell window. 
</p>
<br />

<p>
<img src="https://i.imgur.com/5sVds9j.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we’ll focus on filtering SSH traffic using Wireshark. At this point, you should already be somewhat familiar with navigating Wireshark’s interface. To get started, open the Command Prompt on your Windows computer and initiate an SSH connection to the Linux machine by typing the following command: ssh labuser2@10.0.0.5. Once the connection is established, Wireshark will begin capturing and displaying the SSH traffic, giving you the opportunity to monitor and analyze it in real time. When you’re finished, simply type exit to close the SSH session with the Linux machine.
</p>
<br />

<p>
<img src="https://i.imgur.com/WlKABeY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we’ll focus on filtering DNS traffic in Wireshark. Begin by configuring Wireshark to show only DNS-related packets. To create some DNS activity, you can use the nslookup command, such as nslookup www.yahoo.com. This command sends a query to the DNS server to retrieve the IP address associated with Yahoo’s website. This will help you observe and analyze how DNS requests and responses are handled in the network.
</p>
<br />

<p>
<img src="https://i.imgur.com/afL911f.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next, we’ll use Wireshark to filter and analyze DHCP traffic. DHCP, which stands for Dynamic Host Configuration Protocol, is responsible for automatically assigning IP addresses to devices on a network. To create some DHCP traffic, you can run the command ipconfig /renew in PowerShell. This command will prompt your device to request a new IP address from the DHCP server. As this happens, Wireshark will capture the DHCP activity, allowing us to examine the process in detail.
</p>
<br />

<p>
<img src="https://i.imgur.com/KUhVqBe.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Finally, we’ll set up a filter in Wireshark to capture RDP traffic. Since we’re using Remote Desktop Protocol to connect to our virtual machine, we should see a steady stream of RDP-related data, giving us plenty of information to analyze.
</p>
<br />
