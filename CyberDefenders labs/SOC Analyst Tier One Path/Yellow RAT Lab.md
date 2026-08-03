# Yellow RAT Lab Write-up [CyberDefenders]


<img width="1100" height="247" alt="image" src="https://github.com/user-attachments/assets/caeb68e2-3733-4dca-9b66-7044bf487d36" />

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

<img width="1100" height="566" alt="image" src="https://github.com/user-attachments/assets/d9dd11f6-99eb-461c-867a-54c0c6761e7b" />
And when using HybridAnalysis, I also noticed the file pertains to the Jupyter family, and more specifically, this file pertains to the Yellow-Cockatoo threat actor.

<img width="1100" height="240" alt="image" src="https://github.com/user-attachments/assets/f6bb6b93-712d-41df-b013-d2e591759592" />

---

**Q2: As part of our incident response, knowing common filenames the malware uses can help scan other workstations for potential infection. What is the common filename associated with the malware discovered on our workstations?**

You can see the name of the **dll** under the MD5 hash:


<img width="1100" height="197" alt="image" src="https://github.com/user-attachments/assets/c909623a-4a0f-4173-911c-ddae51eb31e3" />

---

**Q3: Determining the compilation timestamp of malware can reveal insights into its development and deployment timeline. What is the compilation timestamp of the malware that infected our network?**

When searching for the compilation timestamp, I checked for the portable executable details

<img width="1100" height="256" alt="image" src="https://github.com/user-attachments/assets/028da60a-e0a0-4222-84e5-08a21ebf12ac" />

---
**Q4: Understanding when the broader cybersecurity community first identified the malware could help determine how long the malware might have been in the environment before detection. When was the malware first submitted to VirusTotal?**

When checking the history of the file, I can see when the file was first uploaded to VirusTotal.


<img width="738" height="133" alt="image" src="https://github.com/user-attachments/assets/29d9ebe0-5a01-496b-8d61-385c338b6bf5" />

---

**Q5: To completely eradicate the threat from Industries’ systems, we need to identify all components dropped by the malware. What is the name of the .dat file that the malware dropped in the AppData folder?**

When reading Red Canary’s report on the Yellow-Cockatoo RAT, we can see that the solarmarker.dat file was dropped the AppData folder

Reference: https://redcanary.com/blog/threat-intelligence/yellow-cockatoo/

---

**Q6: It is crucial to identify the C2 servers with which the malware communicates to block its communication and prevent further data exfiltration. What is the C2 server that the malware is communicating with?**

When viewing community posts on VirusTotal, I can see the domain of the C2 server

<img width="1100" height="564" alt="image" src="https://github.com/user-attachments/assets/2c717f46-acf3-4a8b-a589-e709ad7a1eeb" />

Additionally, Red Canary’s report also states the the C2 server’s domain is hxxps[://]gogohid[.]com

---
This concludes my write-up.





