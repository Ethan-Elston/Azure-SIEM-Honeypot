# Creating and configuring the SIEM (Microsoft Sentinel)

## Steps

	- The purpose of the SEIM is to visualize the attack data 

	- To do this I searched "Sentinel" in the search bar in Azure
		○ Which I guessed it's called "Microsoft Sentinel" now

	- Just like the other instances I need to click the create button at the top
		○ Then I have the option to connect to whichever log analytic workspace I need to
		○ In this case I have only one…law-SIEMhoneypotLab1

	- Once I select it, I need to click the add button at the bottom

![image](https://github.com/user-attachments/assets/67a97b75-7496-4ea6-a1f9-8d16b22344e7)

	- It will take a while for it to add Microsoft Sentinel to the workspace

	- Once successful, it navigates me to the SIEM News and Guides tab
		○ If I go to the overview tab I can see what I imagine a SIEM dashboard would look like, providing a simple way to view all kinds of information at once

![image](https://github.com/user-attachments/assets/30f72641-4b7c-4f60-9f6c-0aed533c2680)

	- The SIEM is now created

Logging Into the VM for First Time:

	- To log into the VM, I need to go back to where my virtual machines are listed
		○ To do this, just like anything in Azure I'm finding out; I can just search it at the top search bar

	- Once again I search for virtual machines, and once I click on it, I can see a list of all available virtual machine instances

	- Clicking on it, displays everything I need to know about the VM, and a bunch of different configuration options

![image](https://github.com/user-attachments/assets/51f4d429-d77b-4ff2-b07e-626d2465ef7b)

	- I'm finding out that Azure if fairly simple to navigate and it follows the same processes for setting up different instances. Once you do one, it's easy to setup a different application

	- I'm going to log into the VM with a remote desktop
		○ So I need to copy the public IP address of the VM from the overview tab
		○ You can see the address above on the right
		○ Its 20.3.140.217

	- So now I'm going to use my own computer to connect to the VM
		○ To do this I click the start menu of my laptop 
		○ Then search for the "Remote Desktop Connection" application

	- When it opened I pasted the public IP address of the honeypot VM into the computer option
		○ I changed the display settings as well so it wouldn't be maximum view on my screen

	- Instead of entering a username and credentials, I just went ahead and click the connect button at the bottom

![image](https://github.com/user-attachments/assets/3ebad072-0d49-4aa0-82fc-9da233353a17)

	- This takes me to a Windows Security tab, where it says I need to enter my credentials
	
	- I want to log in with the administrator account I configured when I created the VM
		○ To do this I need to click "more choices" at the bottom and then select the "Use a different account" option

	- Before I log in with the actual credentials, I'm going to "fail" a login to simulate a attacker 
		○ This is because I want to create a failed login attempt on Windows Event Viewer 

	- After I "fail" a login, I can then enter the credentials I configured for the admin account when I created the VM
		○ I just accept the certificate warning 

![image](https://github.com/user-attachments/assets/927776a7-b59d-4986-b3af-e6dbc2743e67)
![image](https://github.com/user-attachments/assets/2d3ba431-9f54-468f-9079-dca780543786)

	- After that it begins to log me into the VM
		○ I just say no to unnecessary features and then I'm on the desktop as you can see below

![image](https://github.com/user-attachments/assets/9181830c-380f-4273-9756-ba39b25e1436)

	- I went ahead and completed the setup for Edge because I'm going to use it later on
		○ I don't sign in with anything I just complete the setup


Honeypot Windows Event Viewer:

	- Now that I'm successfully logged into the VM, I want to view the failed login log 

	- To do this, I can just open the Windows Event Viewer from the start menu
		○ (In the VM, not my own computer, just to clarify)

	- As you can see below on the left you can view Windows Logs, Applications and Services Logs, etc., using Windows Event Viewer
		○ Under Windows log I want to view the Security logs
		○ Click the Security tab will reveal a number of security events

	- There are lots of security events, but I want to find that one failed login event in particular 
		○ On the right of the event viewer there's a pane of different options, that can help you save, filter, find, view, copy logs
		○ You can see Event Viewer below

![image](https://github.com/user-attachments/assets/2d6b8b5f-b5db-43b3-bcc5-47fcedc64f67)

	- I use the Filter Current Log option on the right
		○ I only want to see logs in the past hour, so I change it from "Anytime" to "Last hour"
		○ A keyword I need is "Audit Failure" 

	- This should be enough to find the failed login event

![image](https://github.com/user-attachments/assets/19fb553f-67c6-41d5-8637-583b78007fa3)

	- I can then successfully see the failed login event from earlier in the list of events
		○ It has an event ID of 4625

![image](https://github.com/user-attachments/assets/f6f86438-09a8-4300-88b7-3dc18662cd61)

	- These are the events that I'm going to want to gather, these are the events that will be generated from real-life attackers failing to login through RDP

	- Clicking on the event, I can see General details about the failed login
		○ This is the information that we need

	- You can see everything you need such as:
		○ The account information for which the login failed, such as the security ID, the account name, and the account domain
		○ Failure information, which basically explains the reason for the event; in this case it was "Unknown username or bad password"

	- We can also view the real good stuff, which is the network information
		○ This includes the workstation name from which the failed login occurred on. In this case it's the name of my laptop
		○ It also includes the Source Network Address, which is my IP address
		
![image](https://github.com/user-attachments/assets/b64e087f-fc9a-4ef3-b95a-35b4551eaba6)
![image](https://github.com/user-attachments/assets/f90d7c19-60b2-41b0-aaf3-4e04d6b455e8)

	- We are going to use this information to find out where attackers are coming from in the real-world

	- The problem is that this information doesn't really have anything else except their IP address, there's no geographic location information to use

	- To find this information, I'm going to use their IP addresses in conjunction with custom PowerShell scripts from the instructor, to use with a third-party IP/Geolocation API
		○ The website is ipgeolocation.io
		○ You can see it below

![image](https://github.com/user-attachments/assets/bf918922-64f0-4401-8ca2-fa1a62b661cc)

	- As you can see it automatically had my IP address, and therefore all the information needed about my location (this is from the browser of my actual computer)

	- So I'll put the attackers IP addresses into the API, and the API will return the information above
		○ This includes the country
		○ The state/province
		○ The latitude/longitude
		○ The time zone

	- Something interesting that I noticed is that it even has my internet service provider. I just switched to another provider, it's scary how accurate it is

	- The reason I'm going to use custom PowerShell scripts from the instructor is because I'm going to take the information from Windows Event Viewer from the VM and use the Geolocation information above from the API and create my own custom logs, that will combine this information
		○ Then I'm going to send these custom logs to my log analytics workspace, which is connected to Sentinel, which will then plot these locations on a map
		
