# RetailBreach Lab Write-Up [Cyber Defenders]
<img width="1908" height="440" alt="image" src="https://github.com/user-attachments/assets/3cf64a2f-5198-45c9-8512-4701214f7fc8" />
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
<img width="1918" height="762" alt="image" src="https://github.com/user-attachments/assets/41b76e33-3966-4c6b-b35a-6b4a53ba87ca" />

---

Q2: The attacker used a directory brute-forcing tool to discover hidden paths. Which tool did the attacker use to perform the brute-forcing?


- Now that we know what the attacker's IP address is, we can conduct further analysis on what tool the attacker used to enumerate we directories.
<img width="1918" height="665" alt="image" src="https://github.com/user-attachments/assets/267b06a5-2c27-4896-98aa-6b1bd534ace6" />

- When searching for http traffic associated with the TA's IP, we can see the enumeration of several different web directories
- Further down, there is a long conversation that shows the successful enumeration of several web directories using gobuster
<img width="1918" height="815" alt="image" src="https://github.com/user-attachments/assets/391a88db-2d5d-4d7e-9c02-1a8188e15b93" />


---

Q3: Cross-Site Scripting (XSS) allows attackers to inject malicious scripts into web pages viewed by users. Can you specify the XSS payload that the attacker used to compromise the integrity of the web application?

- When using the same filter like above, I found 2 HTTP POST requests that add a script into the **/reviews** directory
<img width="1915" height="745" alt="image" src="https://github.com/user-attachments/assets/a5369ad9-708b-4f25-9a2d-20b9e2363b38" />
- Upon further analysis of the HTTP stream, we can find the malicious script embedded in the HTML of the **/reviews** directory

---

Q4: Pinpointing the exact moment an admin user encounters the injected malicious script is crucial for understanding the timeline of a security breach. Can you provide the UTC timestamp when the admin user first visited the page containing the injected malicious script?

- I found this question to be somewhat difficult.
- To find the exact time an administrator would encounter the malicious script, we need to search for the specific directory where the malicious script was injected

<img width="1918" height="426" alt="image" src="https://github.com/user-attachments/assets/51b9d29b-cd9c-4038-a969-f49493d3c463" />

- When viewing the last packet's details, we can view the time in UTC where the admin would view the script
  
---

Q5: The theft of a session token through XSS is a serious security breach that allows unauthorized access. Can you provide the session token that the attacker acquired and used for this unauthorized access?

- When analyzing traffic based on the **reviews.php** directory, I found different traffic associated with the session
<img width="1918" height="560" alt="image" src="https://github.com/user-attachments/assets/90d203b2-ce46-4a38-a848-054f002cacf3" />
- We can see that session token the attacker stole.
<img width="1918" height="707" alt="image" src="https://github.com/user-attachments/assets/7bebafc0-d118-4280-b74a-04a2b60186ce" />



---

Q6: Identifying which scripts have been exploited is crucial for mitigating vulnerabilities in a web application. What is the name of the script that was exploited by the attacker?

- By using the session token, and the attacker's IP address, we can filter for events with these items, and find the malicious script
<img width="1918" height="562" alt="image" src="https://github.com/user-attachments/assets/d2068a0e-3d13-4300-b8f9-887160d72674" />
 
---

Q7: Exploiting vulnerabilities to access sensitive system files is a common tactic used by attackers. Can you identify the specific payload the attacker used to access a sensitive system file?

- By using the same filter, we can also see the sensitive file accessed by the attacker's script.
<img width="1918" height="428" alt="image" src="https://github.com/user-attachments/assets/5eccb522-2e28-46bb-b97a-72494a131e06" />
