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

<h2>Actions and Observations</h2>

In this lab I create a resource group in Azure. I also create a Windows virtual machine and also a Linux virtual machine. I will practice creating a virtual network and subnet for the machines. For security, I am assigning Azure network security groups. 

</p>
<br />

![What we're doing today in lab](https://github.com/user-attachments/assets/73ce2d1c-20e8-48d2-b173-3d31b655d09c)

</p>
<br />

The first step is setting up an resource group in the Asure dashboard. 

</p>
<br />

![Creating resouce group](https://github.com/user-attachments/assets/b6e64a67-aafd-452f-b8fd-e7b3190655f1)

</p>
<br />

Next I create two virtual machines. One is a Linux VM and the other is a Windows VM. 

![Creating Windows VM](https://github.com/user-attachments/assets/c6e82015-4846-4495-babe-33359b4e7f13)

</p>
<br />

I am sure to setup a custom Vnet while setting up the Windows VM 

![Creating new Vnet while creating VM](https://github.com/user-attachments/assets/6aeaf1b5-94c3-4644-9318-9d27d9cdf300)

</p>

![Naming new Vnet](https://github.com/user-attachments/assets/ab2ceb89-65da-4d75-bb20-82cd188cd243)

</p>
<br />

Next, I setup the Linux VM and select the resource group I created initially and the cusotmer Vnet. 

![Creating Linux VM on same RG and Vnet](https://github.com/user-attachments/assets/bba42509-105d-479d-ae71-f0ba9ad09f3a)

</p>
<br />

After setting up both VMs I make sure they are on the same subnet

![After setting up borth make sure they are on the same subnet](https://github.com/user-attachments/assets/838b68c0-8d2f-4f2e-872d-f95516a33842)

![after setting up both make sure they are on the same subnet windows vm settings](https://github.com/user-attachments/assets/0e0bdf5f-115b-437c-9e69-5f58aaf49486)

<h2>Monitoring Traffic </h2 

I download Wireshark on the Windows VM from the web. 

![Open windows VM and download wireshark](https://github.com/user-attachments/assets/d8af7578-b3f1-4cfc-9c61-adc1ec63e738)

</p>
<br />

Next, I open Wireshark and observe the interface. I also filter the traffic for ICMP only. 

![Wireshark traffic](https://github.com/user-attachments/assets/b79754d2-bfd4-4045-965f-3ff08288c7c4)

![filtering wireshark traffic for icmp only](https://github.com/user-attachments/assets/70783d1f-c0a6-4ed0-8580-88106edb25a7)

</p>
<br />

Now, I can Ping the Linux VM from the Windows VM by usering Powershell. I locate the Linux VM's private IP address under the network settings in Azure. Afterwards I can monitor the ICMP traffic in Wireshark. 


![Pinging the Linux VM from Windows VM in Powershell  Monitring the ICMP traffic in wireshark after](https://github.com/user-attachments/assets/95e62ab3-d707-4790-9d4f-616d151d8fac)


</p>

I initiate a continuous ping using command 10.5.0.2. -t 

</p>

![initiated a continues ping - ping 10 5 0 2 -t and then observe](https://github.com/user-attachments/assets/239efbd5-9a9f-4f56-a5bb-515b67eb39ec)


</p>
<br />

I then adjust the Linux VM firewall rules to clock ICMP traffic. This would block the Pings. Once I confirm the traffic is now blocked in the firewall, I can go to Wireshark to observe if the packets are now being blocked. 


![Adjusting linux vm firewall rules to block icmp traffic -pings](https://github.com/user-attachments/assets/d3d9c8d0-830d-4a92-b631-f964238fc595)

</p>

![Confirmed that traffic is now blocked in firewall](https://github.com/user-attachments/assets/835ccc9d-417c-45de-b52e-0065e8673b99)

</p>

![Packets are being blocked once setting are changed in firewall](https://github.com/user-attachments/assets/95f7380d-06d9-4e0c-b7c5-fa194b66f658)

</p>
<br />

I then deleted the firewall rule then observed to see if the pings start going through. You can see that the readout goes from being timed out to pings going through and getting replies.

![Delete the firewall rule in vm firewall settings which will allow the packets to start being captured again](https://github.com/user-attachments/assets/6f77cc20-e6cb-4a5c-bce9-7ad255cf077a)




































