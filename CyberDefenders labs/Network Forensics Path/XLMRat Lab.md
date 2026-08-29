# Overview
- Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/xlmrat/
<img width="1917" height="435" alt="image" src="https://github.com/user-attachments/assets/6027cb20-0b96-4950-a821-541eb8451fbc" />

# Scenario
A compromised machine has been flagged due to suspicious network traffic. Your task is to analyze the PCAP file to determine the attack method, identify any malicious payloads, and trace the timeline of events. Focus on how the attacker gained access, what tools or techniques were used, and how the malware operated post-compromise.

# Tools Used
- Wireshark
- Ipinfo
- VirusTotal

# Question 1 
The attacker successfully executed a command to download the first stage of the malware. What is the URL from which the first malware stage was installed?

- We can see that there is strange http traffic based on the filter.
<img width="1667" height="126" alt="image" src="https://github.com/user-attachments/assets/f96af884-b5d2-4419-82b2-64409d2e7a7f" />

- Additionally, we can also see that there was two GET requests, one retrieving a **.txt** file, and a **.jpg** file.
  - When examing the details of the 2nd GET request packet, we can see the full request URI. 
<img width="1337" height="821" alt="image" src="https://github.com/user-attachments/assets/0a15795e-025b-45f1-8ab0-462b78f2621e" />

# Question 2 
Which hosting provider owns the associated IP address?

- To identify the hosting provider, I used OSINT tools like Ipinfo to find out what the hosting provider is for the domain using the discovered IP address.
<img width="1345" height="787" alt="image" src="https://github.com/user-attachments/assets/e7f5f7b8-dfd7-4720-9e1f-e17d3efaca20" />


# Question 3
By analyzing the malicious scripts, two payloads were identified: a loader and a secondary executable. What is the SHA256 of the malware executable?
- To identify the hash of the file, I examined the contents of the packet with the JPG file.
- I also extracted the contents, and placed them into CyberChef
<img width="961" height="887" alt="image" src="https://github.com/user-attachments/assets/95f79ffd-3290-425d-ba5e-2051f9fec662" />
- We can see the hex bytes show the file as a windows executable file.

# Question 4
What is the malware family label based on Alibaba?
- To find out the malware family label, I used the SHA256 hash in VirusTotal.
- Based on some community posts, we can see what family the malware is affiliated with.
<img width="1507" height="300" alt="image" src="https://github.com/user-attachments/assets/776de11d-cb4a-413c-918f-642170c3d7c1" />

# Question 5
What is the PE header compile (Creation Time) timestamp of the malware?
- To find out what time the malware was created, I checked the details tab on VT.
<img width="1917" height="832" alt="image" src="https://github.com/user-attachments/assets/aba300ea-5f23-4065-8ee6-6612c1e18d74" />


# Question 6
Which LOLBin is leveraged for stealthy process execution in this script? Provide the full path.
- To check what LOLBin the malware leveraged, I checked the last section of the packet's details in Wireshark.
- We can see commands entered by the script, however they seemed to be obfuscated.
<img width="1647" height="712" alt="image" src="https://github.com/user-attachments/assets/680d2a79-99a2-47aa-a38d-2057ec09a1cf" />

- I pasted the command strings into a text editor
<img width="1411" height="346" alt="image" src="https://github.com/user-attachments/assets/b6bc304f-0596-4d44-b7d8-c1a550348e71" />

- I replaced all of the #'s with an empty space.
<img width="1667" height="450" alt="image" src="https://github.com/user-attachments/assets/94a5e23a-b91e-4af7-a952-f54b95dae168" />
- The most notable section is the **$AC** section which shows the LOLBin the malware leveraged.
- We can see that the section **$NA** had the **-replace** flag, which let the attacker use the hastags to split the full path while still having the program execute.
  
# Question 7
The script is designed to drop several files. List the names of the files dropped by the script.

- We can see that the script dropped 3 additional files.
<img width="1857" height="972" alt="image" src="https://github.com/user-attachments/assets/a7400a22-416f-47f2-8395-d495d9268fd5" />





























































