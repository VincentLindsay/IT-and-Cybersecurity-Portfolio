# PsExec Hunt Lab write-up [CyberDefenders]
lab link: [https://cyberdefenders.org/blueteam-ctf-challenges/psexec-hunt/]

---

<img width="1262" height="336" alt="image" src="https://github.com/user-attachments/assets/da0fc84e-7ec6-4bc3-a29c-50c57fcde9b5" />



Scenario: An alert from the Intrusion Detection System (IDS) flagged suspicious lateral movement activity involving PsExec. This indicates potential unauthorized access and movement across the network. As a SOC Analyst, your task is to investigate the provided PCAP file to trace the attacker’s activities. Identify their entry point, the machines targeted, the extent of the breach, and any critical indicators that reveal their tactics and objectives within the compromised environment.

---
Tools Used:

* Wireshark

---
What we know:

* IDS detected potential lateral movement involving PsExec

---

**Q1: To effectively trace the attacker’s activities within our network, can you identify the IP address of the machine from which the attacker initially gained access?**

Upon viewing the Endpoint conversations, we can see that over 38,000 packets were sent between 2 IPv4 addresses.

<img width="1265" height="282" alt="image" src="https://github.com/user-attachments/assets/81874836-61a9-4fbe-a6f5-d4249cbd1b32" />


We can also see in the protocol hierarchy, that server message block (SMB) was the most common TCP protocol.

<img width="1267" height="355" alt="image" src="https://github.com/user-attachments/assets/a5e45a37-abb1-4c1d-a0bb-f6f171443b81" />

We can also view additional SMB traffic that shows that the suspicious domain may have gained unauthorized access to an active directory environment.

<img width="1267" height="360" alt="image" src="https://github.com/user-attachments/assets/848a8455-8329-4517-a054-670f3e5482d2" />

Based on this evidence, we can infer that the domain 10[.]0[.]0[.]130 is the compromised machine.

---

**Q2: To fully understand the extent of the breach, can you determine the machine’s hostname to which the attacker first pivoted?**

When analyzing a TCP stream that pertained to the compromised machine, we can verify that the Threat Actor (TA) gained access.

<img width="1262" height="332" alt="image" src="https://github.com/user-attachments/assets/9797cdbe-2204-4d80-8c55-e3f5cb660a2c" />

We can also view the stream further, potentially giving us the hostname of the machine:

<img width="1267" height="182" alt="image" src="https://github.com/user-attachments/assets/ab779f85-d965-4d77-9831-6377fef7086f" />

We can see that the name of the comprised host is Sales-PC.

---

**Q3: Knowing the username of the account the attacker used for authentication will give us insights into the extent of the breach. What is the username utilized by the attacker for authentication?**

We can see that the name of the user account of the attacker in the following screenshot. Our attacker was able to gain access through the username **ssales**.

<img width="1267" height="195" alt="image" src="https://github.com/user-attachments/assets/3e0704b7-11e3-4674-8576-1b52bb0db287" />

---

**Q4: After figuring out how the attacker moved within our network, we need to know what they did on the target machine. What’s the name of the service executable the attacker set up on the target?**

When viewing the current TCP stream, we can see the TA was able to gain privileged account levels, and created a request to the server to input the file known as PSEXESVC.exe, which Masquerades the legitimate PSEXEC.exe program.

<img width="1272" height="272" alt="image" src="https://github.com/user-attachments/assets/0faed033-62d9-492c-891c-6272d2ddd1a1" />

---

**Q5: We need to know how the attacker installed the service on the compromised machine to understand the attacker’s lateral movement tactics. This can help identify other affected systems. Which network share was used by PsExec to install the service on the target machine?**

<img width="1267" height="181" alt="image" src="https://github.com/user-attachments/assets/6cdc94f2-3336-4ace-95cb-b3fe820eaca9" />

We can see that the attacker used the ADMIN$ network share in order to have the ability to install the malicious service on the target machine.

--- 
**Q6: We must identify the network share used to communicate between the two machines. Which network share did PsExec use for communication?**

Since we know that our TA used the ADMIN$ share, we can reasonably assume that the attack needed some sort of Administrator level network sharing ability.

<img width="1266" height="285" alt="image" src="https://github.com/user-attachments/assets/9252c79e-ea1d-4b08-9e02-7d454cbf476d" />

I reviewed the previous TCP stream and found that the TA used IPC, a default administrative network share that is used for remote administrative activities, such as file sharing.

Source on IPC$ here: https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/inter-process-communication-share-null-session


---

**Q7: Now that we have a clearer picture of the attacker’s activities on the compromised machine, it’s important to identify any further lateral movement. What is the hostname of the second machine the attacker targeted to pivot within our network?**

Since we know that the main protocol used during the compromise was SMB, I used an SMB filter on wireshark to find an additional compromised machine.

<img width="1267" height="507" alt="image" src="https://github.com/user-attachments/assets/9c1b7ac0-8a84-44a5-9cba-2c0c1bb8601a" />

<img width="1267" height="502" alt="image" src="https://github.com/user-attachments/assets/8f0d0abf-35d9-4ca4-9b00-d88ec91bfa9b" />

As a result, I found that the **Marketing-PC** machine was the next machine that was also compromised.


