# Creating a Log Analytics Workspace (LAW)

## Steps

	- The purpose of a log analytics workspace is to ingest logs from the honeypot
		○ It's going to take the Windows event logs, and then using that data, create our own custom log that contains geographic data, so we can find out where the attackers are coming from
		○ This step is needed because Windows event logs doesn't contain this information by default

	- It's essentially a place where the logs will be stored, and where the SIEM (Sentinel) will connect and display the information from these logs into a map

	- I searched for log analytics workspace in the search bar at the top


	- The process for creating this workspace follows the same format as creating the other VM instance

	- I then click the "+Create" button
		○ This takes me to the Create Log Analytics Workspace tab

	- Under resource group I select our already existing resource group, "SIEMhoneypotLab"

	- For the instance name, I type "law-SIEMhoneypotLab1"
		○ Law stands for log analytics workspace

	- For the region I just put the same as the honeypot, US. West 2

	- I then click review and create at the bottom of the screen

	- After validation I can view basic configurations as well as pricing

	- I clicked create at the bottom again to finalize it

![image](https://github.com/user-attachments/assets/59bc1773-ec92-44c5-a84a-35b12a737c58)

Enable Gathering of VM logs from Microsoft Defender for Cloud

	- At the top search bar in Azure, I typed Microsoft Defender and clicked on it

	- I need to enable the ability to gather logs from the Honeypot VM into the log analytics workspace
		○ It has a great dashboard that shows lots of valuable security information
		○ You can even see alerts that show vulnerabilities that might affect certain subscriptions
		○ You can also monitor different subscriptions like AWS accounts and GCP projects

![image](https://github.com/user-attachments/assets/9e2d98c5-b84a-457a-a67d-9475deb9e999)

	- On the left pane I was originally supposed to configure Azure defender and make sure that the log analytics workspace stored all Window's security events
		○ After doing some research it seems that now Microsoft has it automatically set to do this

	- The ability to gather logs from the VM seems automatically set

	- I can guess I can go ahead and connect the log analytics workspace to the virtual machine


Connecting the Log Analytics Workspace to the Honeypot

	- I go back to the log analytics workspace 

	- I click the law-SIEMhoneypotLab1 workspace and displays an overview as well as a multitude of different configurations I can make for the workspace
		○ It has an activity log, access control, as well as a tab to "diagnose and solve problems", etc.

![image](https://github.com/user-attachments/assets/bc22ed45-8335-4eaa-b549-148a60718f96)

	- On left under the Classic tab, I select the option Virtual Machine 

	- Once I click on the tab it brings up a list of virtual machines that we created
		○ The only one we created is the honeypot-VM

	- Once I click the listed VM, at the top I have an option to "Connect"
		○ I also notice a blue message that says "Not connected"
		○ Once I click connect the message says "Connecting…" 

	- It will take a while to connect

	- I can tell it was successful because I got a green notification and I no longer have the option to connect but only to disconnect

![image](https://github.com/user-attachments/assets/57cdd901-211b-405b-bcc5-b1f2ef50a5a6)

	- So I created a log analytics workspace, was supposed to enable the ability of the log workspace to be able to pull logs from the virtual machine but it seems to be automatically set. I might need to go back to that if there's issues in the future, then connected the log analytics workspace to the honeypot virtual machine, so that it can actually begin to ingest logs

	- Now I can set up the SIEM (Sentinel)
