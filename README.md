# azure-network-protocols

<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a Resource Group, then deploy a Windows 10 VM with a new Virtual Network and Subnet. Afterward, create a Linux (Ubuntu) VM in the same Resource Group and Virtual Network, ensuring both VMs are in the same Subnet for communication.
- Use the Windows app to connect to your Windows 10 VM, install and run Wireshark to capture ICMP traffic, then ping the private IP of the Ubuntu VM and a public website like Google, observing the traffic in Wireshark. Filter for ICMP traffic to monitor the ping requests and replies for both internal and external connections.
- Initiate a continuous ping from your Windows 10 VM to your Ubuntu VM, then disable inbound ICMP traffic in the Ubuntu VM's Network Security Group and observe the impact in Wireshark and the ping command. Re-enable ICMP traffic, observe the restored ping functionality, and then stop the ping activity.
- Log into your Windows VM and use Wireshark to capture SSH traffic while connecting to your Ubuntu VM via SSH, observing the commands and responses in Wireshark. Then, filter for DHCP, DNS, and RDP traffic in Wireshark as you renew your IP address, perform DNS lookups for websites like google.com and disney.com, and monitor RDP traffic by filtering for port 3389.

<h2>Actions and Observations</h2>

<p>
<img alt="Screenshot 2024-12-14 at 3 05 00 PM" src="https://github.com/user-attachments/assets/83ab89be-7a57-4fb9-a662-aba3a9f9974a" />


</p>
<p>
To create a Virtual Machine (VM) in Microsoft Azure, first, log into the Azure Portal and create a **Resource Group** to organize your resources. Then, create the VM by selecting your desired **Subscription**, **Resource Group**, and operating system (e.g., Windows 10 or Ubuntu), and configure networking settings such as **Virtual Network** and **Network Security Group**. After reviewing the settings, click **Create** to deploy the VM, and access it via **RDP** (for Windows) or **SSH** (for Linux). Finally, monitor and manage your VM through the **Azure Portal**, where you can start, stop, and scale the VM as needed.
</p>
<br />

<p>
<img <img width="836" alt="Screenshot 2024-12-14 at 11 27 33 AM" src="https://github.com/user-attachments/assets/21020b70-8ef1-42a9-954a-6b260e25923b" />

</p>
<p>
To observe ICMP traffic, install Wireshark on a Windows 10 VM and use it to capture ICMP packets while pinging both an Ubuntu VM's private IP and a public website (e.g., Google). Then, configure the Ubuntu VM's **Network Security Group** (NSG) to block and later re-enable incoming ICMP traffic, observing how these changes affect the ICMP traffic captured in Wireshark and the ping activity on the Windows 10 VM. The ICMP traffic should stop when the firewall blocks it and resume once it's re-enabled.
</p>
<br />

<p>
<img <img width="925" alt="Screenshot 2024-12-14 at 11 57 38 AM" src="https://github.com/user-attachments/assets/b72f80c1-6f9e-4d09-9982-04228337dc18" />

</p>
<p>
To observe SSH traffic, use Wireshark on the Windows VM to filter for SSH packets while connecting to the Ubuntu VM via SSH, noting the traffic as you interact with the Linux terminal. Next, observe **DHCP** traffic by renewing the Windows VM's IP address, **DNS** traffic by using `nslookup` to resolve website IPs, and **RDP** traffic by filtering for port 3389 to see the constant stream of live traffic due to the ongoing nature of the RDP protocol.
</p>
<br />
