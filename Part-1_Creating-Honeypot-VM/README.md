# Creating a Honeypot VM in Azure

## Steps

	- First I had to create a free Azure subscription account


	- This is the machine that is going to be exposed to the Internet with people actively trying to attack it (honeypot)

	- To start I clicked "create" at the top left of the tool bar

	- This brings me to the "Create a virtual machine" tab that you can see below

![image](https://github.com/user-attachments/assets/c1fa63f9-19a6-43cf-9bb9-4c7628702133)

	- As you can see there are lots of different configurations that you can set
		○ You can choose everything from the base operating system to different availability zones, etc. 

	- I then create a new resource group
		○ A resource group is just a logical grouping of resources in Azure that *usually* share the same life span
		○ Everything in this project is going in the same resource group

	- I named this resource group. "SIEMhoneypotLab"

	- Under the Instance details tab, I can configure the name, region, zone, image, and architecture of the VM
		○ The name of the instance will be "honeypot-VM"
		○ For the region, which is where the datacenter is located, I chose US. West 3
		○ I changed the image from Ubuntu to Windows 10 Pro

	- For this it said that the "size" was not supported in the region US. West 3, so I changed it to U.S. West 2
		○ Then it said that the size was not supported in zone 1 of US. West 2 but region 2 was
		○ Once I changed it to region 2 everything worked

	- I then had to set up the administrator account details
		○ This is the username and password that we will use to log into the VM
		○ Username: Neo!_!
		○ Password: !A$XqKShN3D7#sK

	- I leave the rest of the configurations to their default, including allowing inbound port 3389 (RDP)
		○ This means this port is accessible from the public internet
		○ Even though I've allowed this is still gives me this message. "All traffic from the internet will be blocked by default. You will be able to change inbound port rules in the VM > Networking page."
		○ I'll have to change it later

	- I then click "Next: Disk", I leave this tab to it's default configurations

	- Next is the Networking tab, which is where I’m basically configuring the network interface card, and it's where I can change inbound port rules, configure load balancing, etc. 
		○ Under the "NIC network security group" I can change the radio button from "None" to "Basic" to "Advanced", I switched it from basic to advanced
		○ This is kind of like a firewall

	- Under "Configure network security group" I then create a new network security group
		○ This is the firewall that's going to be open for everyone
		○ I delete the default inbound rules, and click  the "+Add an Inbound Rule" button 
		○ I'm going to make it so that it allows anything into the VM

	- For the destination port ranges I put a star * that means "anything"
		○ Also for the priority rule I gave it a 100
		○ The lower the number the higher the priority 
		○ For the name of inbound security rule, I just put "DANGER_ANY"

	- I then click add

	- This is going to allow all traffic from the Internet into our virtual machine
		○ You can see the custom rule below

![image](https://github.com/user-attachments/assets/277139f9-adc5-41ab-9d4b-613064dc22f3)

	- There's also other tabs such as Management, Monitoring, Advanced, and Tags that you can configure for your VM

	- We don't need this for this lab, so I just went straight to the "Review + create" tab

	- After clicking it, it will take a minute to validate
		○ You can then review pricing, and the summarized configurations of your virtual machine as you can see below
		○ After I was done I clicked "Create"
		
![image](https://github.com/user-attachments/assets/b9495af7-e598-4a9e-aa97-2677394c4341)

	- It will take a while for the deployment process

	- The point of this virtual machine is that we want it as discoverable as possible, whether it's TCP pings, SIN scans, ICMP pings
		○ We don't want any traffic dropped because we want it to be discovered as quick as possible

	- While I wait for it to deploy, I'm going to create a log analytics workspace next
