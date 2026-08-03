# Amadey — APT-C-36 Lab Write-up [CyberDefenders]

<img width="1100" height="357" alt="image" src="https://github.com/user-attachments/assets/cf7504cd-31b7-47fb-8c49-fc9e785dfc6d" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/amadey-apt-c-36/

---
Scenario: An after-hours alert from the Endpoint Detection and Response (EDR) system flags suspicious activity on a Windows workstation. The flagged malware aligns with the Amadey Trojan Stealer. Your job is to analyze the presented memory dump and create a detailed report for actions taken by the malware.

---

Since I am not too familiar with Volatility, I used a cheat sheet from the volatility foundation: https://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf

---

**Q1: In the memory dump analysis, determining the root of the malicious activity is essential for comprehending the extent of the intrusion. What is the name of the parent process that triggered this malicious behavior?**

For this question, I utilized the Pstree plugin.


<img width="1100" height="64" alt="image" src="https://github.com/user-attachments/assets/cf9d6c92-14e7-444e-8bd9-11445480c04a" />


<img width="1100" height="164" alt="image" src="https://github.com/user-attachments/assets/67f14410-48d2-4d28-a591-9cb3177dacf2" />

We can see evidence that another process known as lssass.exe attempts to masquerade the legitimate lsass.exe process.

---
**Q2: Once the rogue process is identified, its exact location on the device can reveal more about its nature and source. Where is this process housed on the workstation?**

Since we know the PID of the malicious lssass.exe, we can use the dlllist plugin to identify the absolute path of the process.


<img width="1100" height="151" alt="image" src="https://github.com/user-attachments/assets/5339a884-56a6-4013-9e10-f43e0bd9c13b" />

As a result, we can see that the path is: C:\Users\0XSH3R~1\AppData\Local\Temp\925e7e99c5\lssass.exe

---

**Q3: Persistent external communications suggest the malware’s attempts to reach out C2C server. Can you identify the Command and Control (C2C) server IP that the process interacts with?**

Using the NetScan plugin, we can identify the malicious process, as well as the C2 server’s IP address it interacts with.


<img width="1100" height="70" alt="image" src="https://github.com/user-attachments/assets/14833371-9ca2-4cc3-babc-3f4856780186" />

We can verify this by identifying the PID of the malicious process.


<img width="1100" height="109" alt="image" src="https://github.com/user-attachments/assets/7c6084ff-0754-4156-a2be-f64e5f6c0a33" />

---
**Q4: Following the malware link with the C2C, the malware is likely fetching additional tools or modules. How many distinct files is it trying to bring onto the compromised workstation?**

For this question, I created a memory map of our current memory dump to locate potential HTTP requests.


<img width="1100" height="30" alt="image" src="https://github.com/user-attachments/assets/c4adb359-1022-400c-a14b-543e1c018037" />

We can see 2 different malicious dlls that the C2 fetches.


<img width="1100" height="200" alt="image" src="https://github.com/user-attachments/assets/973d3ba7-6d20-489a-bc04-f10887b02806" />

---

**Q5: Identifying the storage points of these additional components is critical for containment and cleanup. What is the full path of the file downloaded and used by the malware in its malicious activity?**

Using the cmdline plugin, we can see the malicious dlls being executed by rundll32.exe.


<img width="1100" height="115" alt="image" src="https://github.com/user-attachments/assets/201f9762-67b5-4bff-a92d-673cd28a5ed2" />

---
**Q6: Once retrieved, the malware aims to activate its additional components. Which child process is initiated by the malware to execute these files?**

Using the cmdline plugin, we were able to verify that the child process is rundll32.exe

---

**Q7: Understanding the full range of Amadey’s persistence mechanisms can help in an effective mitigation. Apart from the locations already spotlighted, where else might the malware be ensuring its consistent presence?**

For this section, I used the filescan plugin, and utilized grep to search for specifically the lssass.exe file.

<img width="1100" height="70" alt="image" src="https://github.com/user-attachments/assets/4734d370-8f18-4640-bcff-74c3d5b5dc7a" />

We can see that the malware is hiding itself in the Tasks folder of System32.


<img width="1100" height="72" alt="image" src="https://github.com/user-attachments/assets/4bda9765-1037-46cd-9163-7da61d093e62" />

---
This concludes my write-up. 











