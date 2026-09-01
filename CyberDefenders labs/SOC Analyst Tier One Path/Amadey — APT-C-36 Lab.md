# Amadey — APT-C-36 Lab Write-up [CyberDefenders]

<img width="1275" height="412" alt="image" src="https://github.com/user-attachments/assets/dc42accf-3d6a-4302-9632-de2a7e162c34" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/amadey-apt-c-36/

---
Scenario: An after-hours alert from the Endpoint Detection and Response (EDR) system flags suspicious activity on a Windows workstation. The flagged malware aligns with the Amadey Trojan Stealer. Your job is to analyze the presented memory dump and create a detailed report for actions taken by the malware.

---

Since I am not too familiar with Volatility, I used a cheat sheet from the volatility foundation: https://downloads.volatilityfoundation.org/releases/2.4/CheatSheet_v2.4.pdf

---

**Q1: In the memory dump analysis, determining the root of the malicious activity is essential for comprehending the extent of the intrusion. What is the name of the parent process that triggered this malicious behavior?**

For this question, I utilized the Pstree plugin.


<img width="1267" height="270" alt="image" src="https://github.com/user-attachments/assets/37aa352f-0c85-410a-8fcb-6e783c72f734" />



We can see evidence that another process known as lssass.exe attempts to masquerade the legitimate lsass.exe process.

---
**Q2: Once the rogue process is identified, its exact location on the device can reveal more about its nature and source. Where is this process housed on the workstation?**

Since we know the PID of the malicious lssass.exe, we can use the dlllist plugin to identify the absolute path of the process.


<img width="1280" height="191" alt="image" src="https://github.com/user-attachments/assets/08fc7dde-9995-4a2e-a196-360978ca1ff8" />

As a result, we can see that the path is: C:\Users\0XSH3R~1\AppData\Local\Temp\925e7e99c5\lssass.exe

---

**Q3: Persistent external communications suggest the malware’s attempts to reach out C2C server. Can you identify the Command and Control (C2C) server IP that the process interacts with?**

Using the NetScan plugin, we can identify the malicious process, as well as the C2 server’s IP address it interacts with.


<img width="1276" height="272" alt="image" src="https://github.com/user-attachments/assets/4aa97d6f-cc92-4f4b-a5ea-553e1f3f3e69" />

We can verify this by identifying the PID of the malicious process.


<img width="1100" height="109" alt="image" src="https://github.com/user-attachments/assets/7c6084ff-0754-4156-a2be-f64e5f6c0a33" />

---
**Q4: Following the malware link with the C2C, the malware is likely fetching additional tools or modules. How many distinct files is it trying to bring onto the compromised workstation?**

For this question, I created a memory map of our current memory dump to locate potential HTTP requests.


<img width="1277" height="46" alt="image" src="https://github.com/user-attachments/assets/f752d6c9-bbe6-4953-b2b8-0296a5fa95b4" />

We can see 2 different malicious dlls that the C2 fetches.


<img width="1277" height="236" alt="image" src="https://github.com/user-attachments/assets/a1416b52-a583-4189-b94c-838f370a192c" />

---

**Q5: Identifying the storage points of these additional components is critical for containment and cleanup. What is the full path of the file downloaded and used by the malware in its malicious activity?**

Using the cmdline plugin, we can see the malicious dlls being executed by rundll32.exe.


<img width="1267" height="145" alt="image" src="https://github.com/user-attachments/assets/73eab094-2510-4ff3-9710-125e3af99e82" />

---
**Q6: Once retrieved, the malware aims to activate its additional components. Which child process is initiated by the malware to execute these files?**

Using the cmdline plugin, we were able to verify that the child process is rundll32.exe

---

**Q7: Understanding the full range of Amadey’s persistence mechanisms can help in an effective mitigation. Apart from the locations already spotlighted, where else might the malware be ensuring its consistent presence?**

For this section, I used the filescan plugin, and utilized grep to search for specifically the lssass.exe file.

<img width="1277" height="91" alt="image" src="https://github.com/user-attachments/assets/e5918345-382e-409b-a67f-6f4ac122bdde" />

We can see that the malware is hiding itself in the Tasks folder of System32.


<img width="1276" height="90" alt="image" src="https://github.com/user-attachments/assets/c6d98c37-e0d3-401d-9a36-5976bd4459cc" />

---
This concludes my write-up. 











