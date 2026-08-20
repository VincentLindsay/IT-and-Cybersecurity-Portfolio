# Overview
- lab link: https://tryhackme.com/room/posheclipse

- WORK IN PROGRESS

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

















