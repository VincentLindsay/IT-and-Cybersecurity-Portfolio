# Overview
Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/ramnit/
<img width="1897" height="382" alt="image" src="https://github.com/user-attachments/assets/22c04d59-cfa5-4a41-9111-d0237bda020c" />

# Scenario
Our intrusion detection system has alerted us to suspicious behavior on a workstation, pointing to a likely malware intrusion. A memory dump of this system has been taken for analysis. Your task is to analyze this dump, trace the malware’s actions, and report key findings

# Tools Used
Volatilty3
abuseipdb
ipinfo
VirusTotal

# Question 1
**What is the name of the process responsible for the suspicious activity?**
- Intially, I searched for the process using the **pstree** plugin, but I did not find anything.
<img width="1918" height="862" alt="image" src="https://github.com/user-attachments/assets/286fda59-9426-4f76-bddb-6e09efc2a26f" />

- I then checked if there was maybe any command line executions using the **cmdline** plugin.

Interestingly, I found that the user **Alex** had executed a file known as **Chrome.Setup.exe** which attempts to masquerade. 
<img width="1918" height="688" alt="image" src="https://github.com/user-attachments/assets/2168f964-193d-4be1-90f0-699b0244d3fd" />

# Question 2
**What is the exact path of the executable for the malicious process?**
- In the previous screenshot, we can see the exact path for the malicious process.

# Question 3
**Identifying network connections is crucial for understanding the malware's communication strategy. What IP address did the malware attempt to connect to?**

- To identify the external communications, I used the **windows.netstat** plugin.
  - I also verified any connections via the Process ID (PID) of the file: **4628**

<img width="1317" height="92" alt="image" src="https://github.com/user-attachments/assets/79e96600-f621-421b-a893-bd0fcb42a3f9" />

- We can see that the malware made an attempt to connect with the attacker's server.

# Question 4
**To determine the specific geographical origin of the attack, Which city is associated with the IP address the malware communicated with?**

- To find the city that the malware communicated with via the IP address. I used abuseipdb
<img width="1792" height="892" alt="image" src="https://github.com/user-attachments/assets/4cfd009f-bad8-4b37-af58-584cbfcba276" />

- To verify the location of the IP address, I also verified it via ipinfo
<img width="1757" height="777" alt="image" src="https://github.com/user-attachments/assets/71b84c22-5912-4779-a4a4-0cf7b5fee1f2" />

# Question 5
**Hashes serve as unique identifiers for files, assisting in the detection of similar threats across different machines. What is the SHA1 hash of the malware executable?**

- To find the SHA1 hash, I needed to find the memory address of the **ChromeSetup.exe** binary.
  - To find the memory address, I used the **filescan** pluglin, and searched for the binary.
<img width="1131" height="142" alt="image" src="https://github.com/user-attachments/assets/b0277614-3ffd-45f4-a180-dcb51b5d4a3c" />

- Now that I've found the memory address, I can use this to create a dump of the executable file.
<img width="1201" height="172" alt="image" src="https://github.com/user-attachments/assets/93037b6d-66dc-41c8-8dfa-e937586b7db3" />

- Even though the command said that it failed, we can see the generation of the image.
<img width="1215" height="170" alt="image" src="https://github.com/user-attachments/assets/e7963a80-4eb7-4254-b5c4-60e8abd60d81" />

- Using the **Get-FileHash** command, I was able to retrieve the SHA-1 hash of the file.
<img width="1757" height="166" alt="image" src="https://github.com/user-attachments/assets/3a2e6e68-32b3-4697-a5cf-cfcd105f3bc0" />

# Question 6
**Examining the malware's development timeline can provide insights into its deployment. What is the compilation timestamp for the malware?**

- To find the compilation timestamp of the file, I searched on VirusTotal using the filehash.
  - We can see that the file was created on 12/01/2019 at 08:36 UTC
  
<img width="1917" height="1047" alt="image" src="https://github.com/user-attachments/assets/995c38e6-52ee-41c7-a091-c5b927578e35" />

# Question 7
**Identifying the domains associated with this malware is crucial for blocking future malicious communications and detecting any ongoing interactions with those domains within our network. Can you provide the domain connected to the malware?**

- To find the domains associated with the malware, I checked for any relations via VirusTotal on the relations tab. 
<img width="1918" height="963" alt="image" src="https://github.com/user-attachments/assets/b7d66519-52ae-4e79-848c-3282b9cc1cb7" />

- We can see the domains associated with the file, and the domains contacted by the malware.


