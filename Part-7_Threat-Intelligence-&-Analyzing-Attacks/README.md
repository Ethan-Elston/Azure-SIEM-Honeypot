# Performing threat intelligence and analyzing attacks using Microsoft Sentinel

## Steps

Analyzing New Attacks with the Threat Map:

	- Now I'm going to re-run the PowerShell script on the honeypot, to see new attempts and see if our map is documenting them correctly

	- Once again I connect to the VM, using remote desktop connection

	- To make my honeypot even more attractive, I'm going to turn off Windows Firewall on the VM
		○ For demonstration purposes, if I try and ping the VM from own computer using the command prompt, the requests time out. 
		○ You can see below

![image](https://github.com/user-attachments/assets/02b16054-b9ce-45a2-9045-4aee5aa35c55)

	- To fix this, and make it even more vulnerable, I need to open Windows Defender Firewall on the virtual machine, not my own computer

	- Once I click Windows Defender Firewall Properties, I have the option to switch off the Firewall State
		○ I switch the firewall off for the domain profile, the private profile, and public profile
		○ I then click Apply and then OK

![image](https://github.com/user-attachments/assets/44d0d4d3-0102-4d60-b13b-88497d2c8346)

	- Now if I try and ping the VM from my own computer, it should work
		○ Which it does

![image](https://github.com/user-attachments/assets/08ccd18f-4000-425c-85b6-eb8e96b99619)

	- Now I just need to run the script again, in PowerShell ISE and watch the results

![image](https://github.com/user-attachments/assets/7f8d5b9d-0ef6-409e-a0b8-076135b05fe5)

	- I got a few attempts from India when it first started, but it didn't take long before Ukraine started to take over again as you can see above

	- I'm going to let it run for a few hours before I look at the results again

	- So I set the re-fresh rate to 1 hour for the map



	- After about 5.5 hours I opened up the map again, and I was fascinated to see the amount of failed attempts from all over the world

![image](https://github.com/user-attachments/assets/098d832d-25be-46dc-b62b-fa1fb3efb618)

	- Most was from Ukraine, but as the time of this documentation, Russia is quickly catching up
		○ As you can see I got some from Indonesia, India, and Costa Rica

	- I'm going to let it run overnight, and see what new locations there are in the morning


	- And there we have it, I'm using Azure's SIEM to visualize attack data from around the world
