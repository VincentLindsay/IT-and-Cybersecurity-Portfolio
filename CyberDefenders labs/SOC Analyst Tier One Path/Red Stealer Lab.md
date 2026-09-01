# Red Stealer Lab Write-up [CyberDefenders]
<img width="1257" height="367" alt="image" src="https://github.com/user-attachments/assets/ab2c1555-42f7-4654-955a-62e44fbcab8e" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/red-stealer/

---

Scenario: You are part of the Threat Intelligence team in the SOC (Security Operations Center). An executable file has been discovered on a colleague’s computer, and it’s suspected to be linked to a Command and Control (C2) server, indicating a potential malware infection.

Your task is to investigate this executable by analyzing its hash. The goal is to gather and analyze data beneficial to other SOC members, including the Incident Response team, to respond to this suspicious behavior efficiently.

---
Q1: Categorizing malware enables a quicker and clearer understanding of its unique behaviors and attack vectors. What category has Microsoft identified for that malware in VirusTotal?

Given the file hash, I entered the file onto VirusTotal.

<img width="1126" height="81" alt="image" src="https://github.com/user-attachments/assets/4d425cd3-7129-452f-95fa-6d9af37680e9" />

We can see that Microsoft categorizes the malware as a Trojan, more specifically, the Redline infostealer.

---
Q2: Clearly identifying the name of the malware file improves communication among the SOC team. What is the file name associated with this malware?
When checking the details page on VirusTotal, we can see that the file name associated with the malware is known as WEXTRACT.EXE

<img width="920" height="472" alt="image" src="https://github.com/user-attachments/assets/5bcb63b8-2603-4169-a476-a7966b83ee6b" />

---
Q3: Knowing the exact timestamp of when the malware was first observed can help prioritize response actions. Newly detected malware may require urgent containment and eradication compared to older, well-documented threats. What is the UTC timestamp of the malware’s first submission to VirusTotal?

We can see that the malware was first observed in the wild on October 7th, 2023 , but was submitted to VirusTotal on October 6th, 2023.

<img width="775" height="272" alt="image" src="https://github.com/user-attachments/assets/ef3a770c-037d-48e2-bbdd-91e26b987dd3" />

---
Q4: Understanding the techniques used by malware helps in strategic security planning. What is the MITRE ATT&CK technique ID for the malware’s data collection from the system before exfiltration?
When checking the MITRE ATT&CK framework page, I found that the technique ID is T1005: Data from Local System.

---
Q5: Following execution, which social media-related domain names did the malware resolve via DNS queries?
The malware resolved facebook[.]com during its traversal.

<img width="756" height="682" alt="image" src="https://github.com/user-attachments/assets/7cd3d7d8-6447-4660-b153-64bb64542322" />

---
Q6: Once the malicious IP addresses are identified, network security devices such as firewalls can be configured to block traffic to and from these addresses. Can you provide the IP address and destination port the malware communicates with?

* When viewing the behavior section on VirusTotal, I can see that the IP address communicates with 77[.]91[.]124[.]55:19071.
<img width="582" height="402" alt="image" src="https://github.com/user-attachments/assets/2174bbed-7333-4373-895f-e5ba0747dde8" />

---
Q7: YARA rules are designed to identify specific malware patterns and behaviors. Using MalwareBazaar, what’s the name of the YARA rule created by “Varp0s" that detects the identified malware?

On MalwareBazaar, I searched for the malware Based on its SHA256 hash.
<img width="1270" height="102" alt="image" src="https://github.com/user-attachments/assets/8a2523e8-3c49-4f67-8664-6c5af73c76fb" />



When searching for YARA rules created by Varp0s, I found that the YARA rule was detect_Redline_Stealer.
<img width="1266" height="207" alt="image" src="https://github.com/user-attachments/assets/8d1456ee-c59a-4dc1-9c8b-a82170d8144e" />

---
Q8: Understanding which malware families are targeting the organization helps in strategic security planning for the future and prioritizing resources based on the threat. Can you provide the different malware alias associated with the malicious IP address according to ThreatFox?
On ThreatFox, I used the malware:Redline filter.

<img width="1267" height="245" alt="image" src="https://github.com/user-attachments/assets/0e81e6e9-0907-4c9f-832b-dc7889affe6c" />

We can several submissions of the similar malware, and when accessing the details of one of the submissions, we can see the alias of the malware. It is known as RECORDSTEALER.

<img width="1267" height="392" alt="image" src="https://github.com/user-attachments/assets/89937fcd-a7ee-4cfa-83b4-961e8fdc7869" />

---
Q9: By identifying the malware’s imported DLLs, we can configure security tools to monitor for the loading or unusual usage of these specific DLLs. Can you provide the DLL utilized by the malware for privilege escalation?
When viewing the details page on VirusTotal, we can see the DLLs that the malware loads.

<img width="427" height="442" alt="image" src="https://github.com/user-attachments/assets/19f6855e-5612-4589-8046-99b4baa7c9ef" />

The Malware uses the ADVAPI32.dll file.

---
This concludes my write-up. 








