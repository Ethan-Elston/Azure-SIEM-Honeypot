# Integrating custom PowerShell scripts with geolocation API

## Steps

	- I'm going to use the instructors PowerShell script and download it from GitHub

	- On the VM, I navigate to GitHub and find the instructors custom log exporter file for the lab. You can see below.

![image](https://github.com/user-attachments/assets/d67dd398-38bd-4f5b-92a2-d17f8d9feb3b)

	- Once I've found it, next I need to open PowerShell ISE
		○ PowerShell ISE (Integrated Scripting Environment), is mainly for creating, editing, and debugging PowerShell scripts with some added development tools

	- I create a new script using the top toolbar
		○ Instead of downloading the script I just copied the script from GitHub into PowerShell ISE

![image](https://github.com/user-attachments/assets/0dffa12a-538a-4156-aa33-c3a83d392f35)

	- Then I just save this file to the desktop with the name "Log_Exporter"

	- The only thing I need to change about the script is that I need to get my own API key in order to start the process of converting the IP addresses to longitude, and latitude, etc. (So using the API's services.)

	- An API key is like a password that allows one program (PowerShell script) to access another program's data or services (Geolocation service). The API key is essentially like my access card to use the services and get the data I need for my project. Without it, the service won't provide me with the information. I'm basically telling the service "This is me, I have permission to use your service". 

	- To get the API key, all I need to do is sign into the Geolocation service website. At the top of the PowerShell script the instructor has conveniently put the website address
		○ This follows your typical sign in, and I just used a burner email address for this

	- To clarify, I'm doing this on the VM

	- Once I finally signed up using the burner email and creating a password, I was finally able to log in
		○ At the top of the dashboard was my API key as you can see below

![image](https://github.com/user-attachments/assets/a3406edd-fbf3-4032-9e4b-be8d00256a1f)

	- Now I just copy it and replace the default API key in the script with my own in PowerShell ISE

	- Now I should be able to successfully run the script
		○ This script will look through the Windows Event Viewer logs (on the Honeypot VM), and grab all the events of attackers who failed to login, it will grab their IP address, and get the geo-data from the API and then creates a new log file

	- At the top of the PowerShell window I can see a tool bar, among those tools is a green play button. This button will start the script.
		○ Once I click start, the script begins


	- As you can see I haven't even turned the Windows firewall off, and I'm getting bombarded with login attempts from Kyiv City, Ukraine. These are live and real attempts.

![image](https://github.com/user-attachments/assets/2973836a-3c5f-463c-931b-e7e35986daeb)

	- It's so interesting to me how quick the attempts started to flood in

	- The attempts get logged to C:\ProgramData
		○ I have to find it manually using file explorer because it's hidden
		○ If there is no log file, the script will automatically create a default log file (failed_rdp) with some sample records in it, we'll use these same records to train log analytics workspace into making our custom logs

	- The script will log all failed attempts into this failed_rdp file

	- I was really fascinated with what was happening from Ukraine and let it run longer than it should have, but nonetheless we can use the data to train log analytics workspace into creating our custom logs
		○ The location of the file and the files in this directory are below
		○ As you can see it created the failed_rdp file automatically

![image](https://github.com/user-attachments/assets/3b07799a-3c55-40e5-9332-45e592ad831d)

	- You can see the sample records in the failed_rdp file because the sample records are at the top and have different text, after the sample records, all of them are from Kyiv City in Ukraine

![image](https://github.com/user-attachments/assets/b7152b8c-05b9-4882-882e-c8ac982c89a4)

	- Side note: At the very last log before I got bombarded from attempts from Ukraine, if you look carefully you can see my first initial failed login from earlier

	- Now that we have sample and real data to use, we can begin to train log analytics workspace to create our custom logs
