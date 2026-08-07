# IcedID lab description
<img width="1897" height="438" alt="image" src="https://github.com/user-attachments/assets/1dc22dee-0f34-489e-b1b6-14d35642c8a4" />
lab link: https://cyberdefenders.org/blueteam-ctf-challenges/icedid/

# Scenario:
- A cyber threat group was identified for initiating widespread phishing campaigns to distribute further malicious payloads. The most frequently encountered payloads were IcedID. 
You have been given a hash of an IcedID sample to analyze and monitor the activities of this advanced persistent threat (APT) group.


# Tools used
- VirusTotal (VT)
- 


# Question 1
**What is the name of the file associated with the given hash?**

- In this lab, we were given a sample of the IcedIF malware.
  - In VT, we can see specific details about the file, such as the file's name, and type

 <img width="1482" height="956" alt="image" src="https://github.com/user-attachments/assets/dfe68f40-b2f7-4fc6-990a-d444ffbf4c86" />

- We can see that the file is a malicious Microsoft excel (.xlsx) file.
  - Under the names Tab, we can further Identify the name of the file that the hash is associated with.
 
# Question 2
**Can you identify the filename of the GIF file that was deployed?**

- When viewing the malware's relations, we can see that it contacted several domains with a **.GIF** file for deployment.
<img width="1918" height="918" alt="image" src="https://github.com/user-attachments/assets/a70a2bc6-bb5c-4643-877a-e3aa38c611c2" />


- Furthermore, under the dropped files section, we can see the the dropper deployed additional files, along with the **.GIF** file.
<img width="1918" height="857" alt="image" src="https://github.com/user-attachments/assets/12826784-413b-4889-b719-3e49b56b63a1" />

# Question 3
**How many domains does the malware look to download the additional payload file in Q2?**

- I looked at the relations tab, and found that the malware looked at 5 different domains. 

<img width="1805" height="370" alt="image" src="https://github.com/user-attachments/assets/c9b23762-07a5-44e7-86c5-4f50f90a9322" />

# Question 4
**From the domains mentioned in Q3, a DNS registrar was predominantly used by the threat actor to host their harmful content, enabling the malware's functionality. 
Can you specify the Registrar INC?**

- The threat actor used NameCheap to host the server for the malware.

<img width="1836" height="577" alt="image" src="https://github.com/user-attachments/assets/9fd3cc13-2446-41f5-934a-68deefe507e3" />

# Question 5
**Could you specify the threat actor linked to the sample provided?**

- To find the name of the threat actor, I searched for IcedID on Mitre ATT&CK
<img width="1918" height="1001" alt="image" src="https://github.com/user-attachments/assets/a8e77caf-b48b-41db-92f6-1d30209cee58" />

- More specifically, I looked at the groups that used the software.
<img width="1426" height="527" alt="image" src="https://github.com/user-attachments/assets/32209786-6787-4135-a44f-1ca925320ea5" />

- I found that the actor is classified as TA551, associated with GOLD CABIN.

# Question 6
**In the Execution phase, what function does the malware employ to fetch extra payloads onto the system?**

- To find out the function, I had to look at the tria.ge report.

<img width="1507" height="651" alt="image" src="https://github.com/user-attachments/assets/d0ddbf94-35b0-4b91-9def-3ce93045ac1a" />

- We can see that the malware deploys the URLDownloadToFileA function to fetch extra payloads from a URL.


















