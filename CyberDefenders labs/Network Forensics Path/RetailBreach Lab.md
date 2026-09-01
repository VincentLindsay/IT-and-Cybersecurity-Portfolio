# RetailBreach Lab Write-Up [Cyber Defenders]

<img width="1272" height="292" alt="image" src="https://github.com/user-attachments/assets/eabcf7d9-8df9-4840-8ae2-675fda462bb3" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/retailbreach/

---

# Scenario
In recent days, ShopSphere, a prominent online retail platform, has experienced unusual administrative login activity during late-night hours. 
These logins coincide with an influx of customer complaints about unexplained account anomalies, raising concerns about a potential security breach. 
Initial observations suggest unauthorized access to administrative accounts, potentially indicating deeper system compromise.

Your mission is to investigate the captured network traffic to determine the nature and source of the breach. 
Identifying how the attackers infiltrated the system and pinpointing their methods will be critical to understanding the attack's scope and mitigating its impact.


---

# Lab Questions & Answers: 
Q1: Identifying an attacker's IP address is crucial for mapping the attack's extent and planning an effective response. What is the attacker's IP address?

---

- For this lab, we are given a PCAP of the anomlous activity.
- When viewing the conversations between IPs within the PCAP, we can see two different conversations taken place. One conversation involves over 10,000+ packets, while the other has only 179.
- Moreover, we can also see that the first IP address of the first conversation is sending numerous packets to the other domain.
- We can reasonably assume the IP address of the TA is the first IP address in the first conversation.
<img width="1267" height="505" alt="image" src="https://github.com/user-attachments/assets/c850710c-ac2d-405f-a639-a2dfee7e121a" />

---

Q2: The attacker used a directory brute-forcing tool to discover hidden paths. Which tool did the attacker use to perform the brute-forcing?


- Now that we know what the attacker's IP address is, we can conduct further analysis on what tool the attacker used to enumerate we directories.
<img width="1272" height="432" alt="image" src="https://github.com/user-attachments/assets/74f3ba23-840e-4c96-b223-96cec9e5736c" />

- When searching for http traffic associated with the TA's IP, we can see the enumeration of several different web directories
- Further down, there is a long conversation that shows the successful enumeration of several web directories using gobuster
<img width="1262" height="536" alt="image" src="https://github.com/user-attachments/assets/6ca0a8fe-4279-496a-8ff1-e6f00e0f79dc" />


---

Q3: Cross-Site Scripting (XSS) allows attackers to inject malicious scripts into web pages viewed by users. Can you specify the XSS payload that the attacker used to compromise the integrity of the web application?

- When using the same filter like above, I found 2 HTTP POST requests that add a script into the **/reviews** directory
<img width="1267" height="497" alt="image" src="https://github.com/user-attachments/assets/3cbde356-1a84-40ed-8fb4-229cc1d7df27" />


- Upon further analysis of the HTTP stream, we can find the malicious script embedded in the HTML of the **/reviews** directory

---

Q4: Pinpointing the exact moment an admin user encounters the injected malicious script is crucial for understanding the timeline of a security breach. Can you provide the UTC timestamp when the admin user first visited the page containing the injected malicious script?

- I found this question to be somewhat difficult.
- To find the exact time an administrator would encounter the malicious script, we need to search for the specific directory where the malicious script was injected

<img width="1272" height="281" alt="image" src="https://github.com/user-attachments/assets/72a2d0f4-d84c-467b-8944-842e7ec53d2c" />

- When viewing the last packet's details, we can view the time in UTC where the admin would view the script
  
---

Q5: The theft of a session token through XSS is a serious security breach that allows unauthorized access. Can you provide the session token that the attacker acquired and used for this unauthorized access?

- When analyzing traffic based on the **reviews.php** directory, I found different traffic associated with the session
<img width="1267" height="365" alt="image" src="https://github.com/user-attachments/assets/6433bd4f-77d6-43a4-bf89-a2b2b0c417ff" />


- We can see that session token the attacker stole.
<img width="1272" height="467" alt="image" src="https://github.com/user-attachments/assets/7cc0a8a3-0d92-4e3d-b6eb-ca05eff2d50f" />



---

Q6: Identifying which scripts have been exploited is crucial for mitigating vulnerabilities in a web application. What is the name of the script that was exploited by the attacker?

- By using the session token, and the attacker's IP address, we can filter for events with these items, and find the malicious script
<img width="1267" height="380" alt="image" src="https://github.com/user-attachments/assets/5c768ef5-7307-467d-af8e-c4be7d64cc9a" />
 
---

Q7: Exploiting vulnerabilities to access sensitive system files is a common tactic used by attackers. Can you identify the specific payload the attacker used to access a sensitive system file?

- By using the same filter, we can also see the sensitive file accessed by the attacker's script.
<img width="1267" height="290" alt="image" src="https://github.com/user-attachments/assets/73293b58-a5d5-4322-94f3-b587ba83357e" />
