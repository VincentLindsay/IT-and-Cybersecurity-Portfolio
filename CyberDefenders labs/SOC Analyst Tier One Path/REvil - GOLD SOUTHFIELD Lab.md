# Overview
- lab link: https://cyberdefenders.org/blueteam-ctf-challenges/revil-gold-southfield/
<img width="1918" height="435" alt="image" src="https://github.com/user-attachments/assets/0ac8cb43-f54a-4574-8711-1f882dd63dfa" />

# Scenario
You are a Threat Hunter working for a cybersecurity consulting firm. One of your clients has been recently affected by a ransomware attack that caused the encryption of multiple of their employees' machines. The affected users have reported encountering a ransom note on their desktop and a changed desktop background. You are tasked with using Splunk SIEM containing Sysmon event logs of one of the encrypted machines to extract as much information as possible.

# Tools used
- Splunk SIEM
  - For this lab, we are given the option to use either Splunk, or elastic.
    - I chose to use Splunk for this lab.  

# Question 1 
To begin your investigation, can you identify the filename of the note that the ransomware left behind?

- When searching for **Sysmon** event code 11, which pertains to the creation or writting of a file.
<img width="1918" height="848" alt="image" src="https://github.com/user-attachments/assets/601df7f5-4ae3-4ff9-bc96-869a50a629a9" />

- We can see the note left in numerous directories.

```Splunk Query:
index=revil source="winlog.ndjson"   "event.code"=11 
| sort -time
| stats count by _time, winlog.event_data.TargetFilename
```

# Question 2
After identifying the ransom note, the next step is to pinpoint the source. What's the process ID of the ransomware that's likely involved

- By using a keyword search of the ransom note, we can see the Process ID.
  - We can also see the name of the executable file. 
<img width="1083" height="272" alt="image" src="https://github.com/user-attachments/assets/12a8fd44-d708-49ee-84ea-92af47deac82" />

```Splunk Query
index=revil source="winlog.ndjson" 5uizv5660t-readme.txt
| sort -time
| stats count by winlog.event_data.TargetFilename
```

# Question 3
Having determined the ransomware's process ID, the next logical step is to locate its origin. Where can we find the ransomware's executable file?

- By using the same query in Question 2, I looked at the raw events to find the executable.
<img width="1082" height="272" alt="image" src="https://github.com/user-attachments/assets/f1d9491f-2d25-45c4-bea6-cf74e78c9116" />

# Question 4
Now that you've pinpointed the ransomware's executable location, let's dig deeper. It's a common tactic for ransomware to disrupt system recovery methods. Can you identify the command that was used for this purpose?

- By checking for new created processes via PowerShell, I noticed a command encoded in base64
<img width="1917" height="1005" alt="image" src="https://github.com/user-attachments/assets/dea5cafe-89fb-4fd7-8876-f376b90fe23c" />

- We can see that the ransomware enumerates any shadow copies, deletes them.
 <img width="1918" height="1002" alt="image" src="https://github.com/user-attachments/assets/9cb0967a-4fd6-48b2-88bf-80d2b7980c2c" />

 ```Splunk Query
index=revil source="winlog.ndjson"  powershell
| stats  count by _time, winlog.event_data.CommandLine
| sort -time
```
<img width="1917" height="905" alt="image" src="https://github.com/user-attachments/assets/c5290da1-a0e3-4ea2-b27e-7788835e3e7d" />


# Question 5
As we trace the ransomware's steps, a deeper verification is needed. Can you provide the sha256 hash of the ransomware's executable to cross-check with known malicious signatures?

- To obtain the file's hash, I used the following query:
```Splunk Query
index=revil source="winlog.ndjson"  "winlog.event_data.Image"="C:\\Users\\Administrator\\Downloads\\facebook assistant.exe"  "winlog.event_data.ProcessId"=5348 Hashes
```

- This query will identify the Hashes associated with the file.
<img width="1917" height="993" alt="image" src="https://github.com/user-attachments/assets/e224075d-34f7-488e-ba23-025de23e41ee" />

- By expanding the event log, we can see the SHA-256 hash.

# Question 6
One crucial piece remains: identifying the attacker's communication channel. Can you leverage threat intelligence and known Indicators of Compromise (IoCs) to pinpoint the ransomware author's onion domain?

- To find the IoC's, I used tria.ge using the SHA256 hash.
<img width="1247" height="880" alt="image" src="https://github.com/user-attachments/assets/77a8a9b8-194a-47a6-8c23-eb8cd56b6ab5" />

- By looking at the attributes of the ransom note, we can see the attacker's channel.

