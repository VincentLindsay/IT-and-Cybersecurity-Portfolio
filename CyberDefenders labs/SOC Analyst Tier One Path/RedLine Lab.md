# Overview
lab link: https://cyberdefenders.org/blueteam-ctf-challenges/redline/
<img width="1902" height="553" alt="image" src="https://github.com/user-attachments/assets/df0a570a-deb6-4964-bb38-51dda3f6a246" />

# Scenario
As a member of the Security Blue team, your assignment is to analyze a memory dump using Redline and Volatility tools. Your goal is to trace the steps taken by the attacker on the compromised machine and determine how they managed to bypass the Network Intrusion Detection System (NIDS). Your investigation will identify the specific malware family employed in the attack and its characteristics. Additionally, your task is to identify and mitigate any traces or footprints left by the attacker.

# Tools used
- Volatility: version 3 


# Question 1 
What is the name of the suspicious process?

- In this lab, we are given a memory dump, and to identify if the memory dump is a Windows, or Linux image, I used the **Banners plugin**
<img width="962" height="155" alt="image" src="https://github.com/user-attachments/assets/22e2534d-756f-42c4-bcf2-60e7006ab0e5" />

- We can see that the memory dump is a Windows image due the the letters **NT**.
  - To find the name of the suspicious process, I used the **windows.psTree** plugin.
 
<img width="1926" height="151" alt="image" src="https://github.com/user-attachments/assets/0d567662-427e-47cb-bedf-c125a1af1235" />


 
# Question 2
**What is the child process name of the suspicious process?**

- We can see the suspicious process with an Process ID of **5896**, and a Parent Process ID of **8844**
  - Furthermore, we can also see that the parent process is **rundll32.exe**
<img width="1596" height="92" alt="image" src="https://github.com/user-attachments/assets/bb193b0e-1e74-437a-99a5-605df0c16802" />


# Question 3
**What is the memory protection applied to the suspicious process memory region?**

- To identify the memory region, I used the **windows.malfind.Malfind** plugin.
  - Note: the plugin will be re-named to **windows.malware.malfind.Malfind**
<img width="1901" height="170" alt="image" src="https://github.com/user-attachments/assets/0ab6c1b8-75d2-41bb-ad37-4338171a20c5" />
 
- Going back to finding the memory address of the process, I found that the process has ** PAGE_EXECUTE_READWRITE** protections.
<img width="1345" height="847" alt="image" src="https://github.com/user-attachments/assets/c2684b3e-7ee6-4568-bc53-6c80ab307982" />

- According to Microsoft, this means that the process has Just in Time permissions, meaning that it can read, write, and execute simultaneously.
 - Source: https://learn.microsoft.com/en-us/windows/win32/memory/memory-protection-constants

# Question 4 
**What is the name of the process responsible for the VPN connection?**

- I utilized the **windows.netscan.NetScan** plugin to identify any VPN connections.
  - Interestingly, I found a process named **tun2socks.exe**. 
<img width="1257" height="73" alt="image" src="https://github.com/user-attachments/assets/9cd02d4a-06c5-465d-8b3f-2c63621c7998" />

- I filtered for the process, and we can see the established connections.
<img width="1128" height="162" alt="image" src="https://github.com/user-attachments/assets/1e784734-6707-4ae8-8fdf-44ddee18f803" />

- Going back to the **pslist** plugin, and by filtering the suspicious **tun2socks.exe** process, I found a process associated with it.
<img width="1342" height="150" alt="image" src="https://github.com/user-attachments/assets/6aa39634-070b-4fe5-96d4-0c91320bdf1b" />

# Question 5
**What is the attacker's IP address?**

- To find the attacker's IP address, I used the **netscan** plugin.
<img width="1188" height="133" alt="image" src="https://github.com/user-attachments/assets/715402a5-5c25-4e29-bba4-8a676c585768" />

- We can see the original suspicious process had initiated a connection with a foreign IP address, and utilized HTTP for the connection.

# Question 6 
**What is the full URL of the PHP file that the attacker visited?**
- By using **strings**, and using grep on IP address, I found the full URL.
<img width="647" height="368" alt="image" src="https://github.com/user-attachments/assets/9b4ab8d1-4175-458d-910c-009a50e14879" />


# Question 7 
**What is the full path of the malicious executable?**

- To find the full path of the executable, I used the **filescan** plugin.
<img width="1047" height="72" alt="image" src="https://github.com/user-attachments/assets/3f5ce3c4-6e38-4efb-a74d-150378981921" />

- As a result, I found the full path of the executable.













