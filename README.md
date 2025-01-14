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



</p>
<p>
To create a Virtual Machine (VM) in Microsoft Azure

  Step 1.Log into the Azure Portal

  Step 2.Create a Resource Group to organize your resources. Search resource group, click on icon to open page, hit create on top left, name the resource group and select a region, hit review and create. 
  
  <img width="310" alt="Screenshot 2025-01-14 at 9 54 24 AM" src="https://github.com/user-attachments/assets/4b765764-dc1d-4481-9d6a-dccc95360cb4" />

  Step 3.Create the Windows VM. Search virtual machines, click icon to open page, select create on top left, make sure the correct subscription is selected, select your the previously created resource group, name your VM, select operating system(Windows 10), create a username and password, check box on the bottom left of the page, next go to the network settings ensuring the vnet and IP Address has been created,click review and create, then create to deploy the VM.
  
  <img width="845" alt="Screenshot 2025-01-10 at 1 00 52 PM" src="https://github.com/user-attachments/assets/4a5e12b7-a1fc-4b81-87c3-a72eda980db2" />

Step 4.Create the Linux VM. Select create on the virtual machines page, verify the subscription, select the previously created resource group, select operating system(Unbuntu 22),
select password for security type, use the same username and password used for the Windows VM, go to network settings, verify the vnet is the same vnet as the Windows VM, click review and create, then create to deploy vm.
 
 <img width="451" alt="Screenshot 2025-01-10 at 1 16 01 PM" src="https://github.com/user-attachments/assets/720e37fb-8c08-4d3a-a8df-b7e6e5777d68" /> 

Step 5.Download Windows App to access remote desktop. Within the Windows App click the + icon on top right of screen, selecy add pc, copy the IP Address of the Windows VM in Azure and paste it where it asks for host name/ip address, give it a friendly name, click add.

<img width="453" alt="Screenshot 2025-01-14 at 9 58 49 AM" src="https://github.com/user-attachments/assets/348d2df2-88c2-4f82-87d9-fee54e8f9e13" /> 

Step 6.Login into the Windows VM within the Windows App using the same username and password created when the Windows 10 VM was created.

<img width="453" alt="Screenshot 2025-01-14 at 10 12 16 AM" src="https://github.com/user-attachments/assets/546d324d-a778-4acd-8eb8-c7f85a568958" />

<br />

<p>

</p>
<p>
To Observe the VM's Network Traffic using Wireshark 

  Step 1.After a successful login via Windows App, Search the Wireshark's install website on the Windows 10 VM, select Windows x64 Installer.
  
<img width="763" alt="Screenshot 2025-01-10 at 1 34 53 PM" src="https://github.com/user-attachments/assets/3a99729d-467d-4ccb-b530-14ba0dabdecd" />


Step 2.Open Wireshark and start a packet capture. Click on Ethernet, click blue fin upper left of screen.

![wireshark-start-screen-user-interface-ui](https://github.com/user-attachments/assets/e09b5c10-f436-4c30-842f-8b59a3a04aac)


Step 3.Filter for ICMP traffic. Open Powershell, copy the Linux VM's private IP Address then paste the IP Address in Powershell(ex.ping 10.0.0.5)
</p>

<img width="741" alt="Screenshot 2025-01-10 at 1 44 26 PM" src="https://github.com/user-attachments/assets/519988ca-0763-49af-99d1-42b096f95c0b" />

Step 4.Initiate a nonstop ping within Powershell(ping 10.0.0.5 -t)

<img width="324" alt="Screenshot 2025-01-10 at 1 57 00 PM" src="https://github.com/user-attachments/assets/ca3bb1b4-9352-4a15-8dd4-02124b15c574" />

Step 5.Configure the Network Secruity Group settings on Azure for Linux VM. Inside inbound secruity rules select add rule, deny any inbound network traffic, then analyze the time out request, then delete rule in Azure, go back to Powershell hit keys control + c to stop ping.

<img width="324" alt="Screenshot 2025-01-10 at 1 57 28 PM" src="https://github.com/user-attachments/assets/698fbf97-a2cb-4218-b225-83cc89b30472" />

Step 6. Sign into the Linux VM using Powershell, type (ssh username private IP Addresswhile connecting to the Ubuntu VM via SSH), Filter for SSH in Wireshark,noting the traffic as you interact with the Linux terminal, next type exit to logout of the Linux VM on Powershell. 

<img width="833" alt="Screenshot 2025-01-10 at 3 17 23 PM" src="https://github.com/user-attachments/assets/7c8f5181-b464-4996-999e-e6428043e2da" />


Step 7.Create a notepad file with details (ipconfig /release ipconfig /renew) then save it under cd programdata.

Step 8. Open Powershell as Admin, type cd c:\programdata to configure the IP Address. Within Wireshark filter upd.port = = 67 || upd.port = = 68 to view the DHCP's traffic.

Step 9. Still inside Adminstrator Powershell, type nslookup disney.com to view the IP Address of disney's website. Filter for DNS traffic within Wireshark. Analyze traffic.

<img width="784" alt="Screenshot 2025-01-10 at 3 53 52 PM" src="https://github.com/user-attachments/assets/89fc5bc7-9639-4503-a797-4a776fed0cdc" />


<br />
