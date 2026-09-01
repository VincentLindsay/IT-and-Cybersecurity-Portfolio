# Yellow RAT Lab Write-up [CyberDefenders]


<img width="1180" height="302" alt="image" src="https://github.com/user-attachments/assets/48433e85-23e1-4a6c-b8e1-b48ebba5a70a" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/yellow-rat/

---
Scenario: During a regular IT security check at GlobalTech Industries, abnormal network traffic was detected from multiple workstations. Upon initial investigation, it was discovered that certain employees’ search queries were being redirected to unfamiliar websites. This discovery raised concerns and prompted a more thorough investigation. Your task is to investigate this incident and gather as much information as possible.

---

Tools Used:

* HybridAnalysis
* Red Canary
* VirusTotal
---

**Q1: Understanding the adversary helps defend against attacks. What is the name of the malware family that causes abnormal network traffic?**

Upon initial examination of the MD5 hash, we can see that this file may be a trojan detected on VirusTotal.

<img width="1271" height="651" alt="image" src="https://github.com/user-attachments/assets/11f4fe12-8724-4ce6-afd3-74f54e01a8b0" />

And when using HybridAnalysis, I also noticed the file pertains to the Jupyter family, and more specifically, this file pertains to the Yellow-Cockatoo threat actor.

<img width="1262" height="281" alt="image" src="https://github.com/user-attachments/assets/92ee3a89-f287-4f39-bc32-e1158c1b5fa6" />

---

**Q2: As part of our incident response, knowing common filenames the malware uses can help scan other workstations for potential infection. What is the common filename associated with the malware discovered on our workstations?**

You can see the name of the **dll** under the MD5 hash:


<img width="1262" height="221" alt="image" src="https://github.com/user-attachments/assets/b23cbdc3-8cdb-401e-acee-6ce62b25da3a" />

---

**Q3: Determining the compilation timestamp of malware can reveal insights into its development and deployment timeline. What is the compilation timestamp of the malware that infected our network?**

When searching for the compilation timestamp, I checked for the portable executable details

<img width="1267" height="285" alt="image" src="https://github.com/user-attachments/assets/e8815868-7b53-429b-a042-8744706a4780" />

---
**Q4: Understanding when the broader cybersecurity community first identified the malware could help determine how long the malware might have been in the environment before detection. When was the malware first submitted to VirusTotal?**

When checking the history of the file, I can see when the file was first uploaded to VirusTotal.


<img width="922" height="177" alt="image" src="https://github.com/user-attachments/assets/3eba7aa5-9b72-4176-aeee-143a16d91c55" />

---

**Q5: To completely eradicate the threat from Industries’ systems, we need to identify all components dropped by the malware. What is the name of the .dat file that the malware dropped in the AppData folder?**

When reading Red Canary’s report on the Yellow-Cockatoo RAT, we can see that the solarmarker.dat file was dropped the AppData folder

Reference: https://redcanary.com/blog/threat-intelligence/yellow-cockatoo/

---

**Q6: It is crucial to identify the C2 servers with which the malware communicates to block its communication and prevent further data exfiltration. What is the C2 server that the malware is communicating with?**

When viewing community posts on VirusTotal, I can see the domain of the C2 server

<img width="1316" height="652" alt="image" src="https://github.com/user-attachments/assets/cc6a816e-1557-42f9-b6dd-c5f921fc2818" />

Additionally, Red Canary’s report also states the the C2 server’s domain is hxxps[://]gogohid[.]com

---
This concludes my write-up.





