# Creating custom logs in Log Analytics Workspace

## Steps

	- So I need to go back to Azure on my actual laptop, so that I can create a custom log inside of my log analytics workspace that will have the Geodata

	- Once I navigate to the workspace using the search bar, I click on it and a familiar interface is displayed
		○ On the left under Settings there is tab called Tables
		○ Clicking it will reveal a list of tables and at the top is the ability to create a custom log, as you can see below

![image](https://github.com/user-attachments/assets/eaba6762-487e-440b-af98-94c1403627c0)

	- I had the option to choose between two methods of collecting data DCR and MMA, DCR is the newer way to collect data, but I'm more comfortable with the legacy option MMA which stands for Microsoft Monitoring Agent-based

	- This brings me to the Create a Custom Log page, here I can select a file to upload as the sample file
		○ You can see it below

![image](https://github.com/user-attachments/assets/359efaf4-7863-4041-8aa0-423c60a11a71)

	- The sample log file that I need to upload (failed_rdp) is on the VM and not on my actual laptop
		○ I need to go back to the VM and copy the log and save that log file onto my actual computer

	- I just opened up the failed_rdp file on the VM and copied the sample fail attempts, as well as my one real failed login attempt, as well as a couple real failed logins from Ukraine
		○ I then pasted those logs into notepad on my actual computer and turned off word wrap 
		○ Here it is below on my actual computer

![image](https://github.com/user-attachments/assets/e0937c2c-dbcd-4d35-9345-568c90fb9d1f)

	- I just saved it to the desktop on my physical computer as "failed_rdp.log"

	- Now we finally have data that we can use to train log analytics workspace

	- The reason we're training the workspace, is because we want it to know what to look for in these log files, such as the one above

	- Now I can select a sample log, as you can see below. I successfully uploaded the file from file explorer. 

![image](https://github.com/user-attachments/assets/c43280a0-cfc9-45f7-ab83-5be898d9d354)

	- The next steps are Record delimiter, collection paths, and details
		○ For the record delimiter tab I just skip and review if the logs look correct

	- Now the collection path is important, because this is where the log lives on the VM
		○ Tracing back, I recall that it lives in C:\ProgramData\failed_rdp.log
		○ This needs to be correct, if it's not it won't be able to collect the log. I just went back and checked on the VM to make sure.

	- So for the collection path type, I selected Windows because it's on a Windows machine, and for the path I typed C:\ProgramData\failed_rdp.log

	- On the details tab, I have the ability to name the custom log
		○ I chose the name, "FAILED_RDP_WITH_GEO"

	- After that I can review my configurations on the Review and Create tab
		○ After reviewing I finally click Create at the bottom

	- I can now see my custom table in the list

![image](https://github.com/user-attachments/assets/48f64642-705c-4b8a-9cc6-a74a5ceabd87)

![image](https://github.com/user-attachments/assets/f57309d2-f541-4ed0-b034-54b3397910c0)

	- It will take a minute for the log analytics workspace to sync up with the VM

	- Now I'll go to Logs tab on the left, located just above the Tables tab
		○ Here I can view the logs in log analytics workspace, just like I'm viewing the logs if I was looking at it while on the VM

	- If I just type the custom logs name into the query space I can query for logs after clicking the Run button at the top
		○ After waiting a bit for the LAW to sync with the VM, if I click Run again, I can see the sample logs, as well as the real logs in the results

![image](https://github.com/user-attachments/assets/11c471f7-3dd1-4c19-9279-90cada86a798)

	- If you look at the above screen shot, in the results area, there's a column called RawData
		○ In this column it has all of the Geodata including latitude, longitude information etc. It's essentially each line that we had from the sample logs in notepad.

	- Going back to the VM, if I open the failed_rdp file, remember we can see a long line of data for each attempt that includes the longitude, latitude, source host, destination host, etc. 
		○ The entirety of these long lines of data is what is in the RawData column


Creating Custom Fields:

	- Now we need to create custom fields for our custom logs that now contain geodata
		○ This means I want a separate field for longitude, latitude, source host, destination host, etc. instead of just one column called RawData

	- This is also to make it look nicer

	- So essentially we have to take the raw data and extract certain fields, and use these fields to train log analytics workspace to extract that information and categorize them correctly for future attacks

![image](https://github.com/user-attachments/assets/f8608184-48d4-4691-ac85-705f4e17c6fd)

	- To do this all I need to do is just expand one of logs by clicking the left arrow sign, and then click the 3 dot button

	- So I ran into a problem. The custom field feature of Azure Monitor (MMA) was disabled and they recommended migrating to a DCR-based ingestion-time transformation
		○ https://learn.microsoft.com/en-us/azure/azure-monitor/logs/custom-fields-migrate

	- I have to find another way to create custom fields and "train" log analytics workspace to extract future data correctly

	- Instead I'm just going to use a query I found and extract the data I want from the RawData column
		○ I do this using the following query.
	
	FAILED_RDP_WITH_GEO_CL
		|extend username = extract(@"username:([^,]+)", 1, RawData),
		         timestamp = extract(@"timestamp:([^,]+)", 1, RawData),
		         latitude = extract(@"latitude:([^,]+)", 1, RawData),
		         longitude = extract(@"longitude:([^,]+)", 1, RawData),
		         sourcehost = extract(@"sourcehost:([^,]+)", 1, RawData),
		         state = extract(@"state:([^,]+)", 1, RawData),
		         label = extract(@"label:([^,]+)", 1, RawData),
		         destination = extract(@"destinationhost:([^,]+)", 1, RawData),
		         country = extract(@"country:([^,]+)", 1, RawData)
		 |where destination != "samplehost"
		 |where sourcehost != ""
		 |summarize event_count=count() by timestamp, label, country, state, sourcehost, username, destination, longitude, latitude
		
	- As you can see below this correctly organized and separated the raw data column into the correct "custom fields". We have:
		○ Timestamp
		○ Label
		○ Country
		○ State
		○ Source host
		○ Username
		○ Destination
		○ Longitude
		○ Latitude
		○  Event Count

![image](https://github.com/user-attachments/assets/565ca73a-6737-447b-8c41-a28d9e224cb9)

![image](https://github.com/user-attachments/assets/1aca4669-3480-45b6-8b9f-7b20336d4f63)

	- Since I wasn't able to train the log analytics workspace extracting algorithm, hopefully this query will correctly organize information from future attacks correctly 

