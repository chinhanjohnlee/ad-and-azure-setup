<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Building the Foundation: Preliminary Setup for Active Directory and Network Traffic Analysis between Azure VMs</h1>


<p>Welcome to the inaugural project in a comprehensive series of tutorials focused on Azure and Active Directory implementation. This initial project serves as the foundational cornerstone and setup for the subsequent  parts of this tutorial series. The primary objective is to lay the groundwork for a simple lab environment on Azure to simulate the environment in which Active Directory is employed within an enterprise setting.
</p>

<h2>Overview </h2>

<p>In this first project, I will configure and interconnect two virtual machines, each assuming distinct roles. The first virtual machine will be designated as the Domain Controller. The second virtual machine will be configured as the Client.</p>

<h2>Key Objectives</h2>
<h3>Virtual Machine Setup</h3>

-  Configure the Domain Controller virtual machine
-  Establish the Client virtual machine

<h3>Remote Connectivity</h3>

- Enable a connection using remote desktop connection

<h3> Traffic Inspection</h3>

- Undertake a basic inspection of the network traffic between the Domain Controller and Client virtual machines.



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Configuration Steps</h2>

<h3>&#9312; Create the Domain Controller</h3>

- Create a virtual machine on Azure.
- Name it DC-01 
- Select Windows Server 2022: Azure Edition - x64 Gen2 as the image


<p>
<img width="776" height="154" alt="Image" src="https://github.com/user-attachments/assets/7266569d-0bc4-4a50-ab0e-1e1a6c50dcdb" />
</p>
<p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<strong> NOTE: Make sure to select at least 2 vcpus and 16 GiB memory and take note of the vnet that the VM has created.</strong>
</p>
<br />

<p>
<img width="736" height="62" alt="Image" src="https://github.com/user-attachments/assets/d46c7fc1-57fb-43a0-b764-3b0b45e0c5fd" />
</p>
<p>
</p>
<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9313; Set the Domain Controller's Private IP to static </h3>

-  Once the VM has been deployed, proceed to the VM overview page and select "Networking" on the left side. 
<img width="692" height="397" alt="Image" src="https://github.com/user-attachments/assets/494bf159-75c7-43f1-99de-b2788ed7ad0e" />
<br>
<br>
<br>

-  Select Network Interface Card -> IP configurations -> ipconfig1 and set Private IP address allocation to static.

<br>

<p>
<img width="518" height="161" alt="Image" src="https://github.com/user-attachments/assets/69904514-c8c8-4d9d-a24d-46f405feb419" />
</p>

<br />
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9314; Create the client VM </h3>

- Once again create a new VM and we'll name it Client-01. We'll select Windows 10 as the image and make sure to select at least 2 vcpus and 16 GiB memory.
<img width="717" height="163" alt="Image" src="https://github.com/user-attachments/assets/44acf1e5-3985-4f35-a056-8fb62b55643b" />

<br>
<br>
<br>

<p><strong> NOTE: Make sure to select the same resource group and vnet from the DC-01 VM </strong></p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="731" height="221" alt="Image" src="https://github.com/user-attachments/assets/46bfc1f1-2f09-4820-b509-887a1c4ae118" />

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

- Now finalize everything and wait for its deployment.

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<h3>&#9315; Ensure connectivity between Domain Controller and Client  </h3>

<p>To ensure connectivity between the two VM's, we will ping the domain controller from the client.</p>

- First login to the Client-01 using it's public ip address and remote desktop

<img width="993" height="294" alt="Image" src="https://github.com/user-attachments/assets/2765f2aa-d852-4890-a481-403c4a8010e3" />


<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<img width="297" height="185" alt="Image" src="https://github.com/user-attachments/assets/aa759191-afae-4a13-ba1b-56dcab7551e2" />

<br>
<br>
<br>
<br>
<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Find DC-01's private ip address in the Azure Portal and copy it. Proceed to Client-01 and open the terminal and type "ping -t (DC-01 private ip address)" </strong></p>


<img width="668" height="376" alt="Image" src="https://github.com/user-attachments/assets/785d80c6-a3dd-48f4-ba98-fead2bcf1dcd" />


<br>
<br>

<p> <strong> Now notice how the request timed out, this is because ICMP v4 traffic is blocked by default on DC-01's firewall. So we will have to enable inbound ICMP traffic to allow for Client-01's ping.</strong> </p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Login to DC-01 using remote desktop and open windows defender firewall and select advanced settings. Sort by protocol and find both ICMP echo requests and enable both these rules by right clicking and selecting enable rule.</strong></p>

<br>

<img width="1297" height="809" alt="Image" src="https://github.com/user-attachments/assets/b077d29a-0a5a-47df-afe1-82c68152a78a" />

<br>

<p><strong>.</strong></p>
<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p><strong> Now once the traffic has been enabled, you can check back with Client-01 and notice that the ping is now successful.</strong> </p>

<img width="334" height="380" alt="Image" src="https://github.com/user-attachments/assets/55bd1bd7-4d6e-49af-864e-b264731931a1" />

<h2> Final Thoughts </h2>

<p> We've completed the foundational setup for our Azure and Active Directory project series. By configuring two virtual machines, we've laid the groundwork for implementing the subsequent set of projects. In this project, we focused on establishing a Domain Controller and a Client machine, enabling remote access, and briefly examining network traffic between them. Moving forward, this foundation will help implement more advanced configurations and practical scenarios in Azure and Active Directory. </p>




