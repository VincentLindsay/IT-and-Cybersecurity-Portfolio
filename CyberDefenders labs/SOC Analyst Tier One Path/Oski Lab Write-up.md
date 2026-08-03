# Oski Lab Write-up [CyberDefenders]

**Lab link**: [https://cyberdefenders.org/blueteam-ctf-challenges/oski/]

---

<img width="1100" height="338" alt="image" src="https://github.com/user-attachments/assets/fcdad862-bfbb-4897-91e4-29d27b021f2e" />



Scenario
---
The accountant at the company received an email titled “Urgent New Order” from a client late in the afternoon. When he attempted to access the attached invoice, he discovered it contained false order information.
Subsequently, the SIEM solution generated an alert regarding downloading a potentially malicious file. Upon initial investigation, it was found that the PPT file might be responsible for this download. Could you please conduct a detailed examination of this file?

Investigation
---
Tools used:

* VirusTotal
* Any.Run
---

**Q1: Determining the creation time of the malware can provide insights into its origin. What was the time of malware creation?**

Currently, for this lab, I was given an MD5 hash, and I uploaded the hash to VirusTotal. The hash was detected on VirusTotal as malicious.

<img width="1100" height="522" alt="image" src="https://github.com/user-attachments/assets/b7f6c558-9c0e-4aad-87e4-792fbedbf2cc" />

We can also see that the file may be attributed an infostealer. Additionally, when viewing the details associated with the hash, we can see that the file was created on September 28th, 2022

<img width="1100" height="489" alt="image" src="https://github.com/user-attachments/assets/98692189-72a0-4424-855b-78e3499e0dd3" />

---

**Q2: Identifying the command and control (C2) server that the malware communicates with can help trace back to the attacker. Which C2 server does the malware in the PPT file communicate with?**

When checking for any C2 infrastructure, I noticed that there was two different domains associated with the malware.

<img width="1100" height="344" alt="image" src="https://github.com/user-attachments/assets/e263c260-0a36-4648-a574-896635955ffe" />

From contacted URLs section, I can see that the URL hxxp[://]171[.]22[.]28[.]221/5c06c05b7b34e8e6[.]php pertains to the C2 server utilized by the malware.

Note: the URL was defanged using CyberChef for safety.

---
**Q3: Identifying the initial actions of the malware post-infection can provide insights into its primary objectives. What is the first library that the malware requests post-infection?**


When checking the behavior section on VirusTotal, I found that the malware loads the sqlite3.dll file.

<img width="882" height="493" alt="image" src="https://github.com/user-attachments/assets/89f3ac54-1313-447b-9541-c3842be19619" />

---

**Q4: By examining the provided Any.run report, what RC4 key is used by the malware to decrypt its base64-encoded string?**

In the report, I navigated to the MalConf section of the Any.run report, and found the decrypter RC4 key.

<img width="1100" height="137" alt="image" src="https://github.com/user-attachments/assets/71759688-17c8-4f09-bbd8-5a297f415a04" />

---
**Q5: By examining the MITRE ATT&CK techniques displayed in the Any.run sandbox report, identify the main MITRE technique (not sub-techniques) the malware uses to steal the user’s password.**

In the Any.run report, I can see that the VPN.exe malware attempts to steal web credentials, which correlates to MITRE ATT&CK technique T1555. This technique is the harvesting of credentials from credential stores.

<img width="600" height="392" alt="image" src="https://github.com/user-attachments/assets/08e2c20b-2ac4-4ef6-8e3b-8bf6550e5a4a" />

---
**Q6: By examining the child processes displayed in the Any.run sandbox report, which directory does the malware target for the deletion of all DLL files?**

We can see the the malware targets the C:\ProgramData directory, and attempts to delete all dlls.

<img width="603" height="493" alt="image" src="https://github.com/user-attachments/assets/1598b00b-2d1d-4968-ba96-6b549ed65120" />

---
**Q7: Understanding the malware’s behavior post-data exfiltration can give insights into its evasion techniques. By analyzing the child processes, after successfully exfiltrating the user’s data, how many seconds does it take for the malware to self-delete?**


After the malware spawns the cmd.exe process, it also spawns the timout.exe process that pauses the execution of a process given a set amount of time.

I noticed that the malware specifies** 5 seconds** for timeout.exe to execute.

<img width="607" height="482" alt="image" src="https://github.com/user-attachments/assets/707d3423-ed11-4e51-ad2f-124db7bfd704" />

---

Conclusion:

This malware may could be attributed to be a Malware as a Service (Maas) type of malware, given that each tool detected different families of infostealers.











