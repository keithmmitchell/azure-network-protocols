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
I created a resource group and then a virtual network with the 10.0.0.0/24 address.  Within that network address I create a subnet with the 192.168.1.0/24 address.  I then created two virtual machines, VM1 running Windows 10 and VM2 running Ubuntu. 

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
- Region: (Europ) UK South
- Image: Windows 10 Pro
- Size: Standard_E2s_v3 - 2 vcpus, 16GiB Memory
- Username: labuser1
- Password: Passw0rd1234

Then confirm on the checkbox I have a Windows license and select Next to Disks then Next again to reach Networking.

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/cdb90c7f-65cf-4c9f-bd62-dedee750e64a)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/c41e71bf-3664-4448-a2bd-7af23b8e69c5)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/f84c35b2-8f8b-4487-bdcb-cb90e6a4c0e1)

<p> We can see the subnet is 10.0.0.0/24 and then Review and Create </p>

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/ab90e78a-1ba3-4bd2-829d-e2ddc58d9e7a)

Once it has been validated I then click Create

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/b54359e2-8e38-4151-88fb-de7b8e4a590f)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/b331e87a-7f2b-4630-8a4c-d3ec8e620ed4)

After a few minutes we can see the deployment is complete

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/8fa96292-c9e4-4ab8-8271-0f32a5f0985c)

I then followed the same steps again to create the second virtual machine with the following settings:

- Resource Group: NSGLab
- Virtual Machine Name: VM2
- Region: (Europe) UK South
- Image: Ubuntu Server 22.04
- Size: Standard_E2s_v3 - 2 vcpus, 16GiB memory
- Authentication: Password
- Username: labuser2
- Password: Passw0rd1234
<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/6a789a6a-5220-48a5-b5dd-3b1f261dcadf)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/63c4dbd8-7358-409c-9018-55dd782c0aba)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/4fa6718f-2b2f-4e4b-8f79-686725886f52)



Then select Next for Disks then Next for Networking.  We can see the virtual network, subnet and public IP have been automatically selected so I can then select Review and Create.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/91711f60-dce2-4e4a-91fa-6a78c71e187b)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/a538f852-2fa7-418e-9b51-a9686e06121e)

Once the validation is passed we can then see the deployment complete.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/9ec2e7da-6398-4cfd-8f3e-2aed6218c9d6)

We can then see both machines running in the Virtual Machines blade.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/3ba0e787-b615-46f0-bcae-41f960ebc0cc)

The first thing to do is select VM1 and connect to it via Remote Desktop.  To do this copy the IP address of VM1.


<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/e4cd384e-cef0-4f89-b002-8c63479cf0c8)

Then search for Remote Destop on the physical machine, paste the IP address of the physical machine and click Connect.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/61b1f662-b80e-492f-aab1-4f54f7b64af8)

I am then prompted to enter my password.  Select and More Choices then Use A Different Account.  Type the username labuser1 and the password PAssw0rd1234 then click OK

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/17fe6cc6-97b4-44bc-9a05-b30f9c42251a)

A warning appears saying the identity of the remote computer cannot be idetified but click Yes to connect.  

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/6c817338-1d27-40f2-8c8a-106ce423498e)

Turn off all the privacy settings and click accept.  Click Yes to allow the PC to be discoverable by other PCs and devices on the network.  Open a web browser and search download wireshark.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/74df65ab-6a0a-4a24-89a2-62230291d373)

Then download the Windows installer and click Open File once it has downloaded.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/72ca1d47-0f40-4bc1-8e11-ff7a7bdf7b70)

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/428d15bc-b5e1-4bd3-88f0-28ac88f10207)

On the installation Setup keep pressing Next then click Noted for the License Agreement.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/fc3989fa-47c3-4eaf-b40d-41f859899663)
<p>
  
</p>
<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/dbda6882-54c8-4021-878c-bbf3cec33902)

Then keep clicking Next to choose the default settings.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/aa5d4608-792c-4348-8426-a15a09b54751)

Finally, click on Install.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/78c1f71b-c5d1-406a-962f-c18376dd4a9b)

Click on I Agree for the License Agreement.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/86b3ac64-2469-4571-b56f-fa17b178a444)

Click on Next.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/de4e9cc1-8ede-4b8d-ad18-c72a2941730b)

Then Finish.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/4c45f33b-0857-4730-b44f-31691c760f8e)

Then Next.

<br />

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/4c240239-7ace-4c28-8ca1-d9a983abb930)

Finally, click Finish.

![image](https://github.com/keithmmitchell/azure-network-protocols/assets/174253055/b29bf9c1-bea3-4b76-a449-3c39dd48cfe1)

<br />







































