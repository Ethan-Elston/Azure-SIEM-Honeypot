# Ending notes and cross referencing with MITRE ATT&CK Framework

## Steps

Analysis:

	- Source IP Patterns:

		○  Kyiv City, Ukraine: 185.156.72.37
			§ 6.82k attempts
			§ Used different usernames every time
	
		○ Kyiv City, Ukraine: 31.43.185.40
			§ 820 attempts
			§ Used different usernames every time
	
		○ Central Federal District, Russia: 152.89.198.238
			§ 2.22k attempts
			§ Used different usernames every time
	
		○  Jabodetabek, Indonesia: 36.94.235.50
			§ 85 attempts
			§ Used the same username every time
	
		○ Madhya Pradesh, India: 103.170.58.64
			§ 52 attempts
			§ Used the same username every time
	
		○ San Jose, Costa Rica: 190.112.223.56
			§ 3 attempts
			§ Used the same username everytime
	
	
	- I already know from the geolocation service API what state these IP addresses are correlated with

	- I also know how many attacks are failed attempts were tried from each using the SIEM


Cross Referencing with MITRE Framework:

	- Azure has a built in security coverage using the MITRE ATT&CK Framework
		○ I can use this feature to view the specific techniques and their details

	- TTP's (Techniques, Tactics, and Protocols) Detected (highest # of times detected to lowest):

		○ Initial Access: Valid Accounts (16)
		○ Credential Access: Brute Force (5)
		○ Initial Access: Exploit Public Facing Application (4)
		○ Persistence: Create Account (4)
		○ Command and Control: Application Layer Protocol  (4)
		○ Exfiltration: Data Transfer Size Limits (4)
		○ Impact: Account Access Removal (4)
		○ Execution: Account Manipulation (3)
		○ Execution: Server Software Component (3)
		○ Command and Control: Dynamic Resolution (3)
		○ Persistence: Valid Accounts (2)
		○ Defense Evasion: Impair Defenses (2)
		○ Discovery: Network Service Scanning (2)
		○ Command and Control: Non-Application Layer Protocol (2)
		○ Command and Control: Non-Standard Port (2)
		○ Exfiltration: Exfiltration Over C2 Channel (2)
		○ Exfiltration: Exfiltration Over Other Network Medium (2)
		○ Exfiltration: Exfiltration Over Web Service (2)
		○ Exfiltration: Scheduled Transfer (2)
		○ Exfiltration: Transfer Data to Cloud Account (2)
		○ Initial Access: Drive-by Compromise (1)
		○ Initial Access: External Remote Services (1)
		○ Execution: Command and Scripting Interpreter (1)
		○ Persistence: Office Application Startup (1)
		○ Privilege Escalation: Domain Policy Modification (1)
		○ Privilege Escalation: Valid Accounts (1)
		○ Discovery: Account Discovery (1)
		○ Discovery: Network Share Discovery (1)
		○ Discovery: Permission Groups Discovery (1)
		○ Discovery: Software Discovery (1)
		○ Discovery: Cloud Service Dashboard (1)
		○ Discovery: Cloud Service Discovery (1)
		○ Collection: Data from Information Repositories (1)
		○ Collection: Data Staged (1)
		○ Collection: Email Collection (1)
		○ Collection: Data from Cloud Storage Object (1)
		○ Command and Control: Data Encoding (1)
		○ Command and Control: Data Obfuscation (1)
		○ Command and Control: Encrypted Channel (1)
		○ Command and Control: Fallback Channels (1)
		○ Command and Control: Multi-Stage Channels (1)
		○ Command and Control: Protocol Tunneling (1)
		○ Command and Control: Proxy (1)
		○ Command and Control: Traffic Signaling (1)
		○ Command and Control: Web Service (1)
		○ Impact: Data Destruction (1)
		
		
