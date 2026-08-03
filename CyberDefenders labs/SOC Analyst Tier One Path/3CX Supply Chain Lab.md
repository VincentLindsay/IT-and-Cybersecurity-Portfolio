# 3CX Supply Chain Lab Write-Up [CyberDefenders]

<img width="1100" height="348" alt="image" src="https://github.com/user-attachments/assets/4de8db73-4bac-4ffc-8894-2d5d8bbca44a" />
Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/3cx-supply-chain/

---
Scenario: A large multinational corporation heavily relies on the 3CX software for phone communication, making it a critical component of their business operations. After a recent update to the 3CX Desktop App, antivirus alerts flag sporadic instances of the software being wiped from some workstations while others remain unaffected. Dismissing this as a false positive, the IT team overlooks the alerts, only to notice degraded performance and strange network traffic to unknown servers. Employees report issues with the 3CX app, and the IT security team identifies unusual communication patterns linked to recent software updates.

As the threat intelligence analyst, it’s your responsibility to examine this possible supply chain attack. Your objectives are to uncover how the attackers compromised the 3CX app, identify the potential threat actor involved, and assess the overall extent of the incident.

---
**Q1: Understanding the scope of the attack and identifying which versions exhibit malicious behavior is crucial for making informed decisions if these compromised versions are present in the organization. How many versions of 3CX running on Windows have been flagged as malware?**

When searching for the number of versions of the 3CX malware, I found that there are 2 versions of the malware. I found this via Fortinet's report of the attack.

link:https://www.fortinet.com/blog/threat-research/3cx-desktop-app-compromised

---
**Q2: Determining the age of the malware can help assess the extent of the compromise and track the evolution of malware families and variants. What’s the UTC creation time of the .msi malware?**

Since the lab gave me the actual .msi file, I obtained the SHA-256 file hash using powershell.


<img width="957" height="122" alt="image" src="https://github.com/user-attachments/assets/21162d10-bbb2-468a-a578-e3214782fcb4" />

The file hash will let me conduct further research on the malware. When accessing Virus Total (VT), I found that the malware was created on 2023–03–13 06:33:26 UTC.


<img width="595" height="215" alt="image" src="https://github.com/user-attachments/assets/e5de3fd1-3d30-478b-9bb1-a7da74ff55c5" />

---
**Q3: Executable files (.exe) are frequently used as primary or secondary malware payloads, while dynamic link libraries (.dll) often load malicious code or enhance malware functionality. Analyzing files deposited by the Microsoft Software Installer (.msi) is crucial for identifying malicious files and investigating their full potential. Which malicious DLLs were dropped by the .msi file?**


<img width="1100" height="129" alt="image" src="https://github.com/user-attachments/assets/26708ce1-02d9-43e0-a32e-56ae59cff649" />

When viewing the malware’s behavior on VT, we can see that it spawns two DLLs: ffmpeg.dll, and d3dcompiler_47.dll. I cross referenced the malware’s behavior in the Fortinet article listed above.


<img width="1057" height="412" alt="image" src="https://github.com/user-attachments/assets/3add8b94-064e-4b14-9146-bbbb5fc091ed" />

---

**Q4: Recognizing the persistence techniques used in this incident is essential for current mitigation strategies and future defense improvements. What is the MITRE Technique ID employed by the .msi files to load the malicious DLL?**

When researching the compromise based off of the MITRE technique, I found that the ID is T1574: Hijack Execution Flow: DLL

Link: https://attack.mitre.org/campaigns/C0057/

---

**Q5: Recognizing the malware type (threat category) is essential to your investigation, as it can offer valuable insight into the possible malicious actions you'll be examining. What is the threat category of the two malicious DLLs?**

When checking for the DLLs on VT, I found that the DLLs are categorized as a trojan.


<img width="1100" height="369" alt="image" src="https://github.com/user-attachments/assets/04368c87-db95-40e5-8e73-79e654980539" />

---

**Q6: As a threat intelligence analyst conducting dynamic analysis, it’s vital to understand how malware can evade detection in virtualized environments or analysis systems. This knowledge will help you effectively mitigate or address these evasive tactics. What is the MITRE ID for the virtualization/sandbox evasion techniques used by the two malicious DLLs?**

I found the MITRE ID by searching on google:


<img width="1100" height="332" alt="image" src="https://github.com/user-attachments/assets/5f213039-7405-4ea1-9eca-d4cbd9869a9a" />

---

**Q7: When conducting malware analysis and reverse engineering, understanding anti-analysis techniques is vital to avoid wasting time. Which hypervisor is targeted by the anti-analysis techniques in the ffmpeg.dll file?**

When checking the ffmpeg.dll’s capabilities, I found that it has several abilities, such as host enumeration, and anti-analysis techniques that target VMware.

---

**Q8: Identifying the cryptographic method used in malware is crucial for understanding the techniques employed to bypass defense mechanisms and execute its functions fully. What encryption algorithm is used by the ffmpeg.dll file?**

I can see that the DLL file uses RC4 to bypass defenses.


<img width="400" height="302" alt="image" src="https://github.com/user-attachments/assets/97819af9-a5e5-4017-be17-81944eb6c69f" />

---
**Q9: As an analyst, you’ve recognized some TTPs involved in the incident, but identifying the APT group responsible will help you search for their usual TTPs and uncover other potential malicious activities. Which group is responsible for this attack?**

When reading about the compromise on MITRE Attack, I found that the group involved was AppleJeus, but is under the Lazarus umbrella.

---

This concludes my write-up.



