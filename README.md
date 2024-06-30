<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create resources
- Observe ICMP traffic
- Observe SSH traffic
- Observe DHCP traffic
- Observe DNS traffic
- Observe RDP traffic
- Cleanup
  
<h2>Actions and Observations</h2>

<p>

</p>
<p>
I created a resource group and then a virtual network with the 192.168.0.0/16 address.  Within that network address I create a subnet with the 192.168.1.0/24 address.  I then created two virtual machines, VM1 running Windows 10 and VM2 running Ubuntu. 

To do this I selected Resource Groups from the menu below to bring up the Resource Groups blade.
</p>
<p>
  
![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/0ccc7874-82d4-468a-a8a6-43a3c649ed23)

</p>
<p>We can see currently there are no Resources Groups created so I clicked on the Create button to brin up the Create A Resource Group blade. 
</p>

<p>
  
![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/a1d6e9d8-f1ac-406f-8126-36c5975bf8ea)

</p>
<br />

<p>From there I create a name for the Resource Group, select a Region then Review and Create. </p>
</p>
<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/55514632-c5c7-45fa-8c4d-4c71cea2d7f4)


</p>
<br />

<p>Once the validation is passed I then selected Create </p>

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/64db9512-dc60-4704-9f4b-0eca6e3aef79)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/c36bf4e1-e79c-49de-8e35-618690c81842)

<p>I then start creating the virtual machines by searching for it in the search bar</p>


![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/9ea5227b-1b3c-4103-8c6d-379763e6e583)

<br />
<p>From the Virtual Machines blade I can then select Create Azure Virtual Machine from the centre of the screen </p>

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/0bf39f1e-7d0d-41b8-adf1-804ac50bed1b)
<p></p>

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/a9f2492a-0aea-46d2-97e6-2e314baa7dff)

I then selected the following

- Resource Group: NSGLab
- Virtual Machine Name: VM1
- Image: Windows 10 Pro
- Size: Standard_E2s_v3 - 2 vcpus, 16GiB Memory
- Username: labuser1
- Password: Passw0rd1234

Then confirm on the checkbox I have a Windows license and select Next to Disks then Next again to reach Networking.

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/cdb90c7f-65cf-4c9f-bd62-dedee750e64a)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/c41e71bf-3664-4448-a2bd-7af23b8e69c5)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/f84c35b2-8f8b-4487-bdcb-cb90e6a4c0e1)








