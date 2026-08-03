# PsExec Hunt Lab write-up [CyberDefenders]
lab link: [https://cyberdefenders.org/blueteam-ctf-challenges/psexec-hunt/]

---

<img width="1100" height="281" alt="image" src="https://github.com/user-attachments/assets/8efc13d9-3d2b-4787-aee8-1bd150b4bd23" />


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

<img width="1100" height="244" alt="image" src="https://github.com/user-attachments/assets/1bf77b4c-39b2-42ea-926e-fd7f3b6a86a7" />

We can also see in the protocol hierarchy, that server message block (SMB) was the most common TCP protocol.

<img width="1100" height="304" alt="image" src="https://github.com/user-attachments/assets/4b57b398-c7f1-4bf5-8586-8e54d5d6ccf8" />

We can also view additional SMB traffic that shows that the suspicious domain may have gained unauthorized access to an active directory environment.

<img width="1100" height="310" alt="image" src="https://github.com/user-attachments/assets/91ebe99b-dc7d-4a48-8d87-146701ec7841" />

Based on this evidence, we can infer that the domain 10[.]0[.]0[.]130 is the compromised machine.

---

**Q2: To fully understand the extent of the breach, can you determine the machine’s hostname to which the attacker first pivoted?**

When analyzing a TCP stream that pertained to the compromised machine, we can verify that the Threat Actor (TA) gained access.

<img width="1100" height="282" alt="image" src="https://github.com/user-attachments/assets/b7a03ae4-2569-4d87-98cf-dfa192404cde" />

We can also view the stream further, potentially giving us the hostname of the machine:

<img width="1100" height="156" alt="image" src="https://github.com/user-attachments/assets/16457a33-f175-4e39-9caa-ce8bec0e57c9" />

We can see that the name of the comprised host is Sales-PC.

---

**Q3: Knowing the username of the account the attacker used for authentication will give us insights into the extent of the breach. What is the username utilized by the attacker for authentication?**

We can see that the name of the user account of the attacker in the following screenshot. Our attacker was able to gain access through the username **ssales**.

<img width="1100" height="164" alt="image" src="https://github.com/user-attachments/assets/008cb404-ac10-4797-ae18-19ffbd989fe0" />

---

**Q4: After figuring out how the attacker moved within our network, we need to know what they did on the target machine. What’s the name of the service executable the attacker set up on the target?**

When viewing the current TCP stream, we can see the TA was able to gain privileged account levels, and created a request to the server to input the file known as PSEXESVC.exe, which Masquerades the legitimate PSEXEC.exe program.

<img width="1100" height="230" alt="image" src="https://github.com/user-attachments/assets/c4f52ada-995e-4b70-b05d-e2904a97afc5" />

---

**Q5: We need to know how the attacker installed the service on the compromised machine to understand the attacker’s lateral movement tactics. This can help identify other affected systems. Which network share was used by PsExec to install the service on the target machine?**

<img width="1100" height="154" alt="image" src="https://github.com/user-attachments/assets/71ecbfec-9a38-432a-ba41-a07269275251" />

We can see that the attacker used the ADMIN$ network share in order to have the ability to install the malicious service on the target machine.

--- 
**Q6: We must identify the network share used to communicate between the two machines. Which network share did PsExec use for communication?**

Since we know that our TA used the ADMIN$ share, we can reasonably assume that the attack needed some sort of Administrator level network sharing ability.

<img width="1100" height="239" alt="image" src="https://github.com/user-attachments/assets/d7744462-23fc-4cba-bdf3-da40c96001cf" />

I reviewed the previous TCP stream and found that the TA used IPC, a default administrative network share that is used for remote administrative activities, such as file sharing.

Source on IPC$ here: https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/inter-process-communication-share-null-session


---

**Q7: Now that we have a clearer picture of the attacker’s activities on the compromised machine, it’s important to identify any further lateral movement. What is the hostname of the second machine the attacker targeted to pivot within our network?**

Since we know that the main protocol used during the compromise was SMB, I used an SMB filter on wireshark to find an additional compromised machine.

<img width="1100" height="436" alt="image" src="https://github.com/user-attachments/assets/df72030a-4432-46f6-9aa6-d28ef9b4f290" />

<img width="1100" height="436" alt="image" src="https://github.com/user-attachments/assets/363ed40f-20a7-4720-b778-ee8db0324443" />

As a result, I found that the **Marketing-PC** machine was the next machine that was also compromised.


