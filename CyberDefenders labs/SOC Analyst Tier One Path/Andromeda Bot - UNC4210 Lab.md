# Overview
- Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/andromeda-bot-unc4210/
<img width="1918" height="428" alt="image" src="https://github.com/user-attachments/assets/bbb1d7af-3692-4d33-90e8-2ab0970757e9" />

# Scenario
As a member of the DFIR team at SecuTech, you're tasked with investigating a security breach affecting multiple endpoints across the organization. Alerts from different systems suggest the breach may have spread via removable devices. You’ve been provided with a memory image from one of the compromised machines. Your objective is to analyze the memory for signs of malware propagation, trace the infection’s source, and identify suspicious activity to assess the full extent of the breach and inform the response strategy.

# Question 1
Tracking the serial number of the USB device is essential for identifying potentially unauthorized devices used in the incident, helping to trace their origin and narrow down your investigation. What is the serial number of the inserted USB device?

- To identify the USB device's serial number, I used MemProcFS to mount the image and create forensic timelines.
<img width="1918" height="946" alt="image" src="https://github.com/user-attachments/assets/3ae9dadc-59aa-41df-af83-eb8331cf38dc" />

- Once loaded, I was able to view the memory dump, and identify the USB device.
<img width="1918" height="950" alt="image" src="https://github.com/user-attachments/assets/720cc54b-f7ac-4f22-bd44-51b78fc35774" />

# Question 2 
Tracking USB device activity is essential for building an incident timeline, providing a starting point for your analysis. When was the last recorded time the USB was inserted into the system?

- By looking at the log associated with the USB device, I was able to find the timeline with the first, and last insertion of the USB device.
<img width="1307" height="792" alt="image" src="https://github.com/user-attachments/assets/dd70cfad-3f74-4b11-b24c-9825a46ae0f5" />

# Question 3
Identifying the full path of the executable provides crucial evidence for tracing the attack's origin and understanding how the malware was deployed. What is the full path of the executable that was run after the PowerShell commands disabled Windows Defender protections?

- I created a CSV using Evtxcmd to analyze in Timeline Explorer
<img width="1918" height="203" alt="image" src="https://github.com/user-attachments/assets/b164d16f-7153-4adb-a058-7055338f5a54" />

- In Timeline Explorer, I searched for PowerShell commands.
<img width="1918" height="757" alt="image" src="https://github.com/user-attachments/assets/146f7a58-beec-4ddc-8004-69f5f825d8ea" />

- I found executed commands that disabled real-time monitoring by Windows Defender.
  - Furthermore, I found that the command launches Trusted Installer, a masqueraded process mimicking the Trusted Installer process.
<img width="1918" height="827" alt="image" src="https://github.com/user-attachments/assets/53f52e5a-ad12-4b78-bfcc-2b3e469f6da8" />
 
# Question 4
Identifying the bot malware’s C&C infrastructure is key for detecting IOCs. According to threat intelligence reports, what URL does the bot use to download its C&C file?

- When looking at the log in Timeline Explorer, I found an MD5 hash, and uploaded the file hash to VirusTotal
<img width="1918" height="942" alt="image" src="https://github.com/user-attachments/assets/561d1963-50a8-4c74-a8fb-abd4c67de07c" />


- The hash associated with the "Trusted Installer" process was detected on VT as malicious.
<img width="1918" height="986" alt="image" src="https://github.com/user-attachments/assets/c5e53e82-8f65-4b41-977e-2210f20fb0a4" />

- When checking the relations associated with the bot, I found several contacted URL's.
<img width="1862" height="565" alt="image" src="https://github.com/user-attachments/assets/fff26d90-0700-4573-9b9d-15b15dcc001c" />

# Question 5
Understanding the IOCs for files dropped by malware is essential for gaining insights into the various stages of the malware and its execution flow. What is the MD5 hash of the dropped .exe file?

- To find any other files associated with the initial process, I filtered for "Trusted Installer" logs.
<img width="1918" height="812" alt="image" src="https://github.com/user-attachments/assets/193b56f5-00fb-425e-ba55-d5788f5c8911" />

- Interestingly, I found another file that is associated with the malware.
  - I searched the log for any potential hashes associated with the file.
<img width="1918" height="937" alt="image" src="https://github.com/user-attachments/assets/ea3a0dcd-db98-41e2-bb3b-3bbdeb0fef0d" />
 
# Question 6
Having the full file paths allows for a more complete cleanup, ensuring that all malicious components are identified and removed from the impacted locations. What is the full path of the first DLL dropped by the malware sample?

- To search for the full file path, I checked the original "Trusted Installer" fragments to identify any potential DLLs.
  - Since we are have Sysmon logs available, I checked for any File creations.
 <img width="1918" height="948" alt="image" src="https://github.com/user-attachments/assets/411e05fe-349d-46ae-8e6b-d2a14d72e749" />

- I found the files that were created by the original process.

# Question 7
Connecting malware to APT groups is crucial for uncovering an attack's broader strategy, motivations, and long-term goals. Based on IOCs and threat intelligence reports, which APT group reactivated this malware for use in its campaigns?

- To find out what group the malware is associated with, I googled the **.dll** from the prior question.
- I found the malware is associated with UNC-4210: Turla
link: https://www.nec.com/en/global/solutions/cybersecurity/blog/240823/index.html


