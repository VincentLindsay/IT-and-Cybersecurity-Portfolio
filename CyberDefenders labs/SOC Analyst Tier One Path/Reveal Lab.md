# Overview
lab link: https://cyberdefenders.org/blueteam-ctf-challenges/reveal/

<img width="1918" height="427" alt="image" src="https://github.com/user-attachments/assets/ad8b08f2-b749-4dff-9f75-fafd09a5827f" />

# Scenario
You are a forensic investigator at a financial institution, and your SIEM flagged unusual activity on a workstation with access to sensitive financial data. Suspecting a breach, you received a memory dump from the compromised machine. Your task is to analyze the memory for signs of compromise, trace the anomaly's origin, and assess its scope to contain the incident effectively.

# Tools used
- volatility3

# Question 1
Identifying the name of the malicious process helps in understanding the nature of the attack. What is the name of the malicious process?

- To find the malicious process, I utilized the **windows.pslist** plugin.
  - We can see a suspicious process known as **wordpad.exe** that spawned powershell.exe. 
<img width="1139" height="202" alt="image" src="https://github.com/user-attachments/assets/8e9a3d76-1247-4119-8d9a-32b0fad10c4b" />


# Question 2
Knowing the parent process ID (PPID) of the malicious process aids in tracing the process hierarchy and understanding the attack flow. What is the parent PID of the malicious process?

- By looking at the Process list, I found that the PPID of **powershell.exe**, and **wordpad.exe** shared a similar PPID.
<img width="1139" height="202" alt="image" src="https://github.com/user-attachments/assets/9012db8d-398a-49bd-ba94-7b8feb2eb561" />

# Question 3
Determining the file name used by the malware for executing the second-stage payload is crucial for identifying subsequent malicious activities. What is the file name that the malware uses to execute the second-stage payload?

- By using using the **windows.pstree** plugin, and the PID of **powershell.exe** (3692), I was able to find another interesting process.
<img width="1666" height="141" alt="image" src="https://github.com/user-attachments/assets/8258d6f6-9a07-4d36-b814-2dc50735dfb2" />

- Since I see **conhost.exe** being associated with the **net.exe**, process, I used the **windows.cmdline** plugin to find anything suspicious.
  - We can see the execution of PowerShell to retrieve the second-stage payload from their C2 server.
<img width="1251" height="58" alt="image" src="https://github.com/user-attachments/assets/cfecf416-69a7-4b33-9682-e0f39f4e0f3e" />



# Question 4
Identifying the shared directory on the remote server helps trace the resources targeted by the attacker. What is the name of the shared directory being accessed on the remote server?

- We can see the IP address of the remote server, as well as the shared directory that was accessed by the initial payload to load the second payload on the victim's machine.
<img width="1251" height="64" alt="image" src="https://github.com/user-attachments/assets/210e0c25-faf1-4ba9-98f8-e19567af2a79" />

# Question 5
What is the MITRE ATT&CK sub-technique ID that describes the execution of a second-stage payload using a Windows utility to run the malicious file?

- Since the attacker utilized **rundll32** to execute the second-stage payload, we can recognize that the attacker utilized LOLBins.
<img width="1542" height="890" alt="image" src="https://github.com/user-attachments/assets/542e69b9-4fef-4ea4-ab18-01fbadcf124e" />

# Question 6
Identifying the username under which the malicious process runs helps in assessing the compromised account and its potential impact. What is the username that the malicious process runs under?

- To identify the username associated with the malicious process, I used the **windows.getsids** plugin.
<img width="1001" height="305" alt="image" src="https://github.com/user-attachments/assets/02267864-9c7e-4b71-8ab1-a4d19f998337" />

# Question 7 
Knowing the name of the malware family is essential for correlating the attack with known threats and developing appropriate defenses. What is the name of the malware family?

- Since we know the IP address of the remote server, I can use OSINT tools like VirusTotal to identify the name of the malware's family.
<img width="1882" height="747" alt="image" src="https://github.com/user-attachments/assets/b7f4f878-2279-42bd-aa8f-933c9f6a72aa" />

- We can see the name of the malware family via the crowsourced context.
