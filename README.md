# Networking-Concepts
<p align="center">

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/8040b061-fa6a-457b-8efd-d340b532285a)

</p>

<h1>Networking Concepts with Wireshark - Prerequisites and Installation</h1>
This tutorial outlines the installation and traffic capture of the open-source packet analyzing system Wireshark.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Wireshark

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Ubuntu Server 20.04

<h2>List of Prerequisites</h2>

- Item 1
- Item 2
- Item 3
- Item 4
- Item 5

<h2>Installation Steps</h2>

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/11542da1-56c1-4577-9be7-870197b7c10b)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/ec7e3428-d1cb-4bb4-972f-5bf1cbc021d7)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/0beb5a3d-74f3-4132-8b3e-e264f1fe2508)


</p>
<p>
To start this project, first create your resource group in Azure. Then, create your Windows 10 VM and set up a user name and password that will be used to connect to it later. The Windows 10 VM will be named "VM1"
</p>
<br />

<p>

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/fa00efe8-1447-49b3-bd90-13b85b8eda67)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/becccac8-cbac-4e4a-8fd7-1c92506439b1)

</p>
<p>
Once the Windows 10 VM has been created, create another VM in Azure that is going to be running Ubuntu Linux. This will be named "VM2". On VM2, make sure your virtual network is created in the same resource group you used for VM1.
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/0129e067-52e3-44cf-b490-72faa39b2fb9)

</p>
<p>
Once both VMs are running, make a note of the private IP address of VM2 (mine is 10.0.0.5) and log into the Remote Desktop Connection using the public IP address of VM1. We will be pinging VM2 from VM1 later on in the lab. 

Inside your VM, search 'Wireshark' in whatever search engine you are using and download the Windows version of the program.  
</p>
<br />

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/54885069-1eb3-42a0-a3f6-65f02be6a218)

</p>
<p>
Inside Wireshark, start off by filtering for ICMP traffic so we can view this traffic while pinging to VM2.
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/55248306-5caa-417b-b2f6-d45d68ccbeec)

</p>
<p>
To ping VM2, open Powershell and type 'ping 10.0.0.5'. Once entered, you should be able to see all of the ICMP traffic that occurred when you pinged to VM2.
</p>
<br />

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/4657fc91-cb0f-4f8d-b5e8-3d2d88a5c677)

</p>
<p>
Continuing with ICMP traffic, we are going to see how changing firewall settings will affect the traffic that is being shown. First, initiate a pertpetual/non-stop ping to VM2 'ping -t 10.0.0.5'. You should see constant traffic flowing on both Powershell and Wireshark.
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/285032e3-b16c-4a8a-a37a-10880e722ed3)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/23f0867d-017a-453a-88ed-052ee6526fd8)


</p>
<p>
On your host machine, go back to Azure and search 'Network Security Groups' and look for security settings for VM2. Go to the 'Inbound security rules' on the left side panel and you will see the current security rules for VM2 traffic. Click 'Add' and select ICMP for the protocol and Deny for your action. Save your new rule and go back to your virtual machine to view the current traffic. Your non-stop ping from earlier should be displaying 'Request timed out' and your Wireshark traffic should be unable to find a response as well. This is because we have block all ICMP traffic on the network. Clear your command line (Ctrl + C) and we will move on to bewing ssh (Secure Shell) traffic.
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/890b7561-8c3d-4a1f-9bec-7e1b02057f5c)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/133e1a4e-ebd2-4bad-8deb-8e5a60dc0eb4)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/c9cb917c-3af5-4c83-807e-be4c30166099)


</p>
<p>
Filter for SSH traffic inside Wireshark. We are going to connect to our VM2 command line from VM1. To do this, inside Powershell type 'ssh labuser@10.0.0.5' with labuser being the username we created and 10.0.0.5 being the private IP address of VM2. Type in the password (note: you may not be able to see the password being entered. Just have faith in what you're typing and if you mess up you can try again.) and you should see yourself connected to the Linux shell (green font). You should also see SSH traffic in Wireshark as you're connected to VM2.
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/5bc03062-2e4b-4624-aeb0-ce0abe20ea84)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/21dd4bc0-2670-4680-9a9c-bee7c57da44e)


</p>
<p>
Next, we will view DHCP traffic. Filter DCHP traffic in Wireshark and we are going to request our VM to issue us a new ip address. In Powershell, type 'ipconfig /renew'. You can see we have some DHCP traffic in Wireshark and a new ip address is showing in our command line. 
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/77ead1d6-aa00-459c-90f2-b5432030bb7a)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/ca365b8c-fb6f-4010-9fa8-2fc41ec0b503)
![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/b71c389a-9fa5-4c30-8870-91871d826844)


</p>
<p>
The next protocol we will look at is DNS. To see how DNS is displayed in Wireshark, go to your command line so we can search the IP address for a website. The first website I used was Google. Enter 'nslookup www.google.com' and you should see the DNS traffic in Wireshark along with the ip address for Google. I did the same thing for Netflix, 'nslookup www.netflix.com'.
</p>
<br />

<p>

![image](https://github.com/jrford32/Networking-Concepts/assets/101678489/e0698b71-8e39-4b6f-879d-69dfba4ff20e)

</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
