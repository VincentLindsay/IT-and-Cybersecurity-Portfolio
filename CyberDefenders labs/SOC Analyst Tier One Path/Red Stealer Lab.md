# Red Stealer Lab Write-up [CyberDefenders]
<img width="1331" height="415" alt="image" src="https://github.com/user-attachments/assets/2b50bf96-7c0c-4f30-bb67-54aa75bdd298" />
lab link: https://cyberdefenders.org/blueteam-ctf-challenges/red-stealer/

---

Scenario: You are part of the Threat Intelligence team in the SOC (Security Operations Center). An executable file has been discovered on a colleague’s computer, and it’s suspected to be linked to a Command and Control (C2) server, indicating a potential malware infection.

Your task is to investigate this executable by analyzing its hash. The goal is to gather and analyze data beneficial to other SOC members, including the Incident Response team, to respond to this suspicious behavior efficiently.

---
Q1: Categorizing malware enables a quicker and clearer understanding of its unique behaviors and attack vectors. What category has Microsoft identified for that malware in VirusTotal?

Given the file hash, I entered the file onto VirusTotal.

<img width="897" height="67" alt="image" src="https://github.com/user-attachments/assets/afc978c0-b39d-4548-95b4-d604a9c49dd9" />

We can see that Microsoft categorizes the malware as a Trojan, more specifically, the Redline infostealer.

---
Q2: Clearly identifying the name of the malware file improves communication among the SOC team. What is the file name associated with this malware?
When checking the details page on VirusTotal, we can see that the file name associated with the malware is known as WEXTRACT.EXE
<img width="737" height="377" alt="image" src="https://github.com/user-attachments/assets/00172aec-a388-4a0a-bee1-53e49b2fbb14" />

---
Q3: Knowing the exact timestamp of when the malware was first observed can help prioritize response actions. Newly detected malware may require urgent containment and eradication compared to older, well-documented threats. What is the UTC timestamp of the malware’s first submission to VirusTotal?

We can see that the malware was first observed in the wild on October 7th, 2023 , but was submitted to VirusTotal on October 6th, 2023.

<img width="620" height="207" alt="image" src="https://github.com/user-attachments/assets/7e209817-fda7-4ab7-9ca4-d7973e75317d" />

---
Q4: Understanding the techniques used by malware helps in strategic security planning. What is the MITRE ATT&CK technique ID for the malware’s data collection from the system before exfiltration?
When checking the MITRE ATT&CK framework page, I found that the technique ID is T1005: Data from Local System.

---
Q5: Following execution, which social media-related domain names did the malware resolve via DNS queries?
The malware resolved facebook[.]com during its traversal.

<img width="753" height="865" alt="image" src="https://github.com/user-attachments/assets/a05f2e9f-b04c-4840-94d2-b3f8d99324b5" />

---
Q6: Once the malicious IP addresses are identified, network security devices such as firewalls can be configured to block traffic to and from these addresses. Can you provide the IP address and destination port the malware communicates with?
When viewing the behavior section on VirusTotal, I can see that the IP address communicates with 77[.]91[.]124[.]55:19071.
<img width="462" height="320" alt="image" src="https://github.com/user-attachments/assets/18df16bb-03a3-464a-9dd4-737ec37c301f" />

---
Q7: YARA rules are designed to identify specific malware patterns and behaviors. Using MalwareBazaar, what’s the name of the YARA rule created by “Varp0s" that detects the identified malware?

On MalwareBazaar, I searched for the malware Based on its SHA256 hash.
<img width="1100" height="85" alt="image" src="https://github.com/user-attachments/assets/9c7e45b7-0492-4e13-875b-780ddbb9a860" />
When searching for YARA rules created by Varp0s, I found that the YARA rule was detect_Redline_Stealer.
<img width="1100" height="176" alt="image" src="https://github.com/user-attachments/assets/7b92aae9-b0cb-4469-a650-00f64dfe6e1a" />

---
Q8: Understanding which malware families are targeting the organization helps in strategic security planning for the future and prioritizing resources based on the threat. Can you provide the different malware alias associated with the malicious IP address according to ThreatFox?
On ThreatFox, I used the malware:Redline filter.

<img width="1100" height="206" alt="image" src="https://github.com/user-attachments/assets/712cd852-e82b-4584-9709-b19a6b018f15" />

We can several submissions of the similar malware, and when accessing the details of one of the submissions, we can see the alias of the malware. It is known as RECORDSTEALER.

<img width="1100" height="340" alt="image" src="https://github.com/user-attachments/assets/3930e7c8-7d8d-4fbc-8b90-c66030979129" />

---
Q9: By identifying the malware’s imported DLLs, we can configure security tools to monitor for the loading or unusual usage of these specific DLLs. Can you provide the DLL utilized by the malware for privilege escalation?
When viewing the details page on VirusTotal, we can see the DLLs that the malware loads.

<img width="328" height="353" alt="image" src="https://github.com/user-attachments/assets/3b70940e-e9a0-46e9-990a-90f83bb84b42" />

The Malware uses the ADVAPI32.dll file.

---
This concludes my write-up. 








