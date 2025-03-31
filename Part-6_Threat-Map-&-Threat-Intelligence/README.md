# Creating and configuring a threat map and performing threat intelligence in Sentinel

## Steps

Setting Up the Threat Map in Sentinel:

	- I left the log analytics workspace tab open, and opened another tab for Sentinel 
		○ Then I click on the LAW that I added to it previously

![image](https://github.com/user-attachments/assets/21204464-f3fc-47ff-bef6-0451c4d729ee)

	- I turned off the "new overview" feature and it displayed events and alerts over time, as well as a map at the bottom

	- I took a break from this lab for a couple days from the last step, when I was creating custom fields, so there is no recent events. 

![image](https://github.com/user-attachments/assets/6da698f4-aa84-4fa7-92c3-38cb7d099d45)

	- To set up the actual Geo map, I used the tab on the left called Workbooks
		○ You can also see tabs for Incidents, Hunting, Entity behavior, Threat intelligence, SOC optimization, Data connectors, Watchlists, Automation, etc. 

	- Workbooks in Azure let you instantly visualize and analyze data so that you can see what's happening across all of your connected data sources. It provides tables, charts, maps, etc., to provide the user with analytics for their logs and queries

	- I need to create a new workbook, there's an option at the top of the window to create a new workbook.
		○ Clicking it displays the New workbook window below

![image](https://github.com/user-attachments/assets/08654650-0836-4e1c-bb1d-ca6ac080b8ae)

	- As you can see there are already default widgets that are displayed
		○ A chart and a table

	- You can also see the FAILED_RDP_WITH_GEO custom log, and how many attempts it's already logged (about 1,400 attempts)

	- I'm going to remove the default widgets using the Edit button at the top
		○ This displays a message saying Sentinel has no content

	- I'm going to add a new query using the add button at the bottom

![image](https://github.com/user-attachments/assets/2c452084-33d1-4c56-9f24-cdf032f9d05e)

	- Now I'm going to use the same query I used in the log analytics workspace. However this time it's in Sentinel, and like last time it will correctly organize the data in the correct fields.
		○ Since I haven't recently ran the script to capture new logs, I had to change the time range to the last 7 days

![image](https://github.com/user-attachments/assets/45925222-5970-4686-9d01-64d2cc03b5eb)

	- As you can see above the query was successful in correctly separating the data in the logs into the correct fields. 


	- Now I want to visualize the data into a map
		○ To do this I just click the Visualization drop down tab at the top
		○ There are a lot of options you can choose from in order to visualize your data, including grids, area charts, bar charts, line charts, pie charts, time charts, tiles, scatter charts, and maps

![image](https://github.com/user-attachments/assets/65c3a6a9-95b9-4c21-87dd-2d68146bc77a)

	- I chose map of course
		○ This displayed the following

![image](https://github.com/user-attachments/assets/02af89db-b2c4-4d6e-9bf3-4dcdeea3c71c)

	- On the right you have map settings, where I can configure what and how the map displays the data

	- You can also see the actual map
		○ A big orange and red spot is over Ukraine (where a majority of the attempts were from)
		○ Two are from France, which was from the sample file, I don't know why the other sample locations aren't listed
		○ One is in Texas, which was me from my single failed login attempt


	- There are a few things I need to change:

	- I changed the map size to full at the top

	- At the bottom of the settings on the right, there is a section called Metric settings
		○ Under the metric label, I can choose one of the custom fields we created
		○ I chose "label", which was the reason for creating this custom field, it shows the country and IP address
		○ For the metric value, I left it to the default setting which was the event count
		○ After clicking apply, under the map it should show the country and IP address, as well as the number of attacks originating from that country (number of events)
		○ You can see below

![image](https://github.com/user-attachments/assets/82a20304-66d6-4737-8daa-421f633e2e17)
![image](https://github.com/user-attachments/assets/b2aae131-9572-4c0c-97d7-21fbc98a8da0)

	- The other default settings seem to be correct
		○ It's sizing the bubbles by event count, which is correct
		○ The color of the bubbles is also correct

	- I just save and close the settings tab

	- It should now look like the following

![image](https://github.com/user-attachments/assets/6339e346-e6bf-41b4-b0c6-821f6c1527d9)

	- Now I need to save the map workbook
		○ I click the save button at the top

	- I save this workbook as "Failed_RDP_WorldMap"
		○ Select the correct resource group, SIEMhoneypotLab
		○ A select the correct location, US West 2

![image](https://github.com/user-attachments/assets/4e84c29e-bfbf-4c6a-bab3-8b05fd0704b1)

	- I now have my map!

![image](https://github.com/user-attachments/assets/4e631215-1df2-4cff-b208-36c8f56cf346)

