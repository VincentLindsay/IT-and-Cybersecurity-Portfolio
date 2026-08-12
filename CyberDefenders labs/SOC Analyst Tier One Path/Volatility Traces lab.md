# Overview
Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/volatility-traces/
<img width="1907" height="407" alt="image" src="https://github.com/user-attachments/assets/f42dadd7-29be-4a1e-aa40-2b020fea7274" />

# Scenario
On May 2, 2024, a multinational corporation identified suspicious PowerShell processes on critical systems, indicating a potential malware infiltration. This activity poses a threat to sensitive data and operational integrity.

You have been provided with a memory dump (memory.dmp) from the affected system. Your task is to analyze the dump to trace the malware's actions, uncover its evasion techniques, and understand its persistence mechanisms.

# Tools used
- Volatility version

# Question 1
**Identifying the parent process reveals the source and potential additional malicious activity. What is the name of the suspicious process that spawned two malicious PowerShell processes?**

- In this lab, we are given a memory dump, and to find the suspicious process that spawned PowerShell, I used the **pslist** plugin.
  - I also used grep to search for any instance of PowerShell spawns. 
<img width="1916" height="101" alt="image" src="https://github.com/user-attachments/assets/1ff6d176-0c3f-4d39-88d4-c2feabdced2a" />

- I found that the PowerShell process has a Parent ID of 4596.
  - I then searched for PowerShell using the PPID with the **pstree** plugin.

<img width="1922" height="262" alt="image" src="https://github.com/user-attachments/assets/2f48ec39-364e-48ca-b06d-77e8a76c2dee" />

- We can see that an exception was given to a suspicious process.

# Question 2
**By determining which executable is utilized by the malware to ensure its persistence, we can strategize for the eradication phase. Which executable is responsible for the malware's persistence?**

- To find the persistence executable, I used the **psscan** plugin, and grepped using the PPID.
<img width="1916" height="372" alt="image" src="https://github.com/user-attachments/assets/04762259-0346-4486-aead-fc09cc5e25bd" />

# Question 3 

**Understanding child processes reveals potential malicious behavior in incidents. Aside from the PowerShell processes, what other active suspicious process, originating from the same parent process, is identified?**

- Using the previous screenshot, we can see another process associated with PPID.
  - the RegSvcs.exe process, refers to the registry service.
<img width="1917" height="362" alt="image" src="https://github.com/user-attachments/assets/badb5bcc-1c24-428f-8b4e-f04739583503" />

# Question 4
**Analyzing malicious process parameters uncovers intentions like defense evasion for hidden, stealthy malware. What PowerShell cmdlet used by the malware for defense evasion?**

- To check for the commandlet, I used the **cmdline** plugin.
<img width="1917" height="145" alt="image" src="https://github.com/user-attachments/assets/2027d853-a29d-41c7-8945-898b8669dc29" />

- We can see that the malware used **Add-MpPreference**, which adds a Windows Defender exception to the malware, which makes it harder to detect.

# Question 5
**Recognizing detection-evasive executables is crucial for monitoring their harmful and malicious system activities. Which two applications were excluded by the malware from the previously altered application's settings?**

- In order to find the additional applications, I used the **cmdline** plugin, and filtering by grepping the **Add-MpPreference** command.
<img width="1917" height="147" alt="image" src="https://github.com/user-attachments/assets/2df51c96-bc93-4d61-a90b-fd0d10b2cf53" />

- We can see that the two additional executable that were added as an exception to Windows Defender.

# Question 6 
**What specific MITRE ATT&CK sub-technique ID describes an adversary configuring exempted folders or path exclusions to hide malicious payloads from security inspection?**
 
- In the MITRE ATT&CK framework, I checked the Tactic of stealth, specifically **T1564** which pertains to the hiding of artifacts.
  - Behavior-wise, we know that the attacker used commands to creation file exclusions.
<img width="1917" height="927" alt="image" src="https://github.com/user-attachments/assets/3a9ee0a8-1302-4045-be0c-8a1ccf358cfb" />
 
# Question 7
**Determining the user account offers valuable information about its privileges, whether it is domain-based or local, and its potential involvement in malicious activities. Which user account is linked to the malicious processes?**

- By checking the **cmdline** plugin, we can see the full path of the file exclusions being added, along with the user account associated with the commands.
<img width="1918" height="122" alt="image" src="https://github.com/user-attachments/assets/c412d0a6-d9d6-40a7-87ca-a168fd927011" />







