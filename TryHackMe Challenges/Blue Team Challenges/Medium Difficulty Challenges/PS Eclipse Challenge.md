# Overview
- lab link: https://tryhackme.com/room/posheclipse



# Scenario
You are a SOC Analyst for an MSSP (Managed Security Service Provider) company called TryNotHackMe .

A customer sent an email asking for an analyst to investigate the events that occurred on Keegan's machine on Monday, May 16th, 2022 . The client noted that the machine is operational, but some files have a weird file extension. The client is worried that there was a ransomware attempt on Keegan's device. 

Your manager has tasked you to check the events in Splunk to determine what occurred in Keegan's device. 

Happy Hunting!

# A suspicious binary was downloaded to the endpoint. What was the name of the binary?
- To accurately identify the activity associated with the binary, I viewed the data sources available in Splunk.
<img width="1007" height="610" alt="image" src="https://github.com/user-attachments/assets/b7f0764e-ddf8-4868-a027-e92b1feaab95" />

- We can see that we have Sysmon logs available, as well as Windows event logs.
  - I also adjusted the date and time to accurately identify events.
<img width="817" height="397" alt="image" src="https://github.com/user-attachments/assets/b56ee01b-2e46-449f-bda4-f171f9404c9a" />

- We can see that a network logon occurred at 13:16 UTC on 05/16/2022
<img width="1918" height="717" alt="image" src="https://github.com/user-attachments/assets/f84a7158-e4a8-4378-bf66-656639fd8a4b" />

- Now that we now there was a remote logon, I checked if there was any downloaded files.
  - Furthermore, by filtering for files executed in the remote session, we can see the suspicious binary.
<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/80a4bc70-aa04-4887-9e52-d13d4c4ce7bc" />
 
# What is the address the binary was downloaded from? 
- To find out the how the attacker downloaded the binary, We need to verify how the attacker retrieved the potential ransomware
<img width="1918" height="386" alt="image" src="https://github.com/user-attachments/assets/9ac0c4f1-afa4-42ac-ac28-3326f085784e" />

- When identifying processes, I found a process associated with the keegan account, so this can become a valuable filtering point.
  - Beginning at 13:27 UTC, we can see the attacker beginning to remove Windows Defender Components
<img width="1662" height="767" alt="image" src="https://github.com/user-attachments/assets/c6eea1ef-32e6-4f21-921c-ce6c7bfec317" />
 
- At 13:29, we can see the attacker begin to execute the encoded powershell script that contains the ransomware.
  <img width="1667" height="830" alt="image" src="https://github.com/user-attachments/assets/76812e75-f058-4cd7-8b99-e80aa8577c43" />

- Furthermore, by taking the encoded script into cyberchef, we can see the entire script, including the malicious address.
<img width="1537" height="967" alt="image" src="https://github.com/user-attachments/assets/01770267-b9c3-4d4d-8c32-c967226c5321" />


# What Windows executable was used to download the suspicious binary? Enter full path
- By looking at the event taken place at 13:29, which pertains to the initial execution of the PowerShell script, we can also reference the time to identify the full path of the Windows executable used in the execution of the ransomware.
<img width="1667" height="772" alt="image" src="https://github.com/user-attachments/assets/0d3a7095-3952-4139-9eff-2713333db60b" />

<img width="1666" height="852" alt="image" src="https://github.com/user-attachments/assets/69c290dc-7c70-4292-a3b9-005809b55d16" />

# What command was executed to configure the suspicious binary to run with elevated privileges?
- To find the exact command to configure the binary, I searched based on the name of the file, as well as any events pertaining to scheduled tasks.
<img width="1667" height="680" alt="image" src="https://github.com/user-attachments/assets/71e3708d-e041-48e9-b0e8-55d4d5b2ee61" />


- We can see the exact command string used by the attacker.

# What permissions will the suspicious binary run as? What was the command to run the binary with elevated privileges? (Format: User + ; + CommandLine)

- To find the exact command that the attacker used, I keyword searched for the binary name.
<img width="1667" height="777" alt="image" src="https://github.com/user-attachments/assets/cc2fca37-3f09-48de-984c-c5adc363afdf" />

- We can see that the file runs as SYSTEM.

# The suspicious binary connected to a remote server. What address did it connect to? Add http:// to your answer & defang the URL.
- To find the exact remote server, I searched for any events that pertained to the malware.
<img width="1667" height="776" alt="image" src="https://github.com/user-attachments/assets/6e7fb4f0-5fa7-499b-9aa6-697371f6b081" />

- We can see 5 events that pertain to a DNS query, and as a result, I filtered for DNS queries.
<img width="1667" height="311" alt="image" src="https://github.com/user-attachments/assets/1598590f-5d72-40d9-91af-c1a691652a20" />

- We can see the exact server the malware connected to.

# A PowerShell script was downloaded to the same location as the suspicious binary. What was the name of the file?
- From what we know, the malware resides in **C:\Windows\Temp**, and since we are looking for a PowerShell script, I searched for files with the **.ps1** extension
<img width="1667" height="496" alt="image" src="https://github.com/user-attachments/assets/9ec9c434-83d0-4e74-827a-0c27c2f54b1a" />


- We can see 5 different scripts, but looking at the time, the script event at 13:37:58 resembles the timeline of the attacker's actions.

The malicious script was flagged as malicious. What do you think was the actual name of the malicious script?

- To identify the actual name of the script, I obtained the MD5 hash of the file, and uploaded it to VirusTotal.
<img width="1666" height="762" alt="image" src="https://github.com/user-attachments/assets/1a2538a9-2846-4ea0-a4c3-23c2877c8f45" />

- We can the actual name of the malicious PowerShell script.
<img width="1917" height="996" alt="image" src="https://github.com/user-attachments/assets/75889b08-2517-4f63-9405-803b273b1391" />

# A ransomware note was saved to disk, which can serve as an IOC. What is the full path to which the ransom note was saved?

- To find the ransom note, I searched for any **.txt** files using the **TargetFilename** field.
<img width="1676" height="777" alt="image" src="https://github.com/user-attachments/assets/fe0c3f4a-9be9-439b-b012-78c652c55567" />

# The script saved an image file to disk to replace the user's desktop wallpaper, which can also serve as an IOC. What is the full path of the image?

- Similarly, I also searched for any **.jpg** files to identify the image file on the machine.
<img width="1675" height="396" alt="image" src="https://github.com/user-attachments/assets/216e0c93-2cb0-4ce6-9da2-9b13d1e2354a" />


























