# PoisonedCredentials Lab Write-up [CyberDefenders]
<img width="1272" height="325" alt="image" src="https://github.com/user-attachments/assets/6b557f41-8a73-4a07-8e24-1a73bf3f8026" />

lab link: [https://cyberdefenders.org/blueteam-ctf-challenges/poisonedcredentials/]

---

Scenario: Your organization’s security team has detected a surge in suspicious network activity. There are concerns that LLMNR (Link-Local Multicast Name Resolution) and NBT-NS (NetBIOS Name Service) poisoning attacks may be occurring within your network. These attacks are known for exploiting these protocols to intercept network traffic and potentially compromise user credentials. Your task is to investigate the network logs and examine captured network traffic.

---

Tools Used:

* Wireshark

Initially, I was not too familiar with LLMNR, however after some research I learned that LLMNR is a protocol that is used as a fallback option when DNS is not available on Windows systems.

Reference: https://tcm-sec.com/llmnr-poisoning-and-how-to-prevent-it/

---

**Q1: In the context of the incident described in the scenario, the attacker initiated their actions by taking advantage of benign network traffic from legitimate machines. Can you identify the specific mistyped query made by the machine with the IP address 192.168.232.162?**

We are given a .PCAP to examine the traffic in this lab

I noticed that there were multiple conversations between multiple machines resembling the IP address listed above.

<img width="1267" height="191" alt="image" src="https://github.com/user-attachments/assets/21900933-1314-4670-adec-3049bf6401c3" />

Upon filtering for specific traffic using the IP address, I found interesting LLMNR queries made by the attacker.


<img width="1267" height="257" alt="image" src="https://github.com/user-attachments/assets/da3d5116-8b80-400b-8c09-62abd0815ff5" />

I found that the attacker may have misspelled a file share name, giving their cover away while using a legitimate machine in the network.

---

**Q2: We are investigating a network security incident. To conduct a thorough investigation, We need to determine the IP address of the rogue machine. What is the IP address of the machine acting as the rogue entity?**

Since I know that the machine with the IP address 192.168.232.162 is a benign machine, I searched for conversations with this machine IP, as well as the LLMNR traffic, and additional responses.


<img width="1265" height="155" alt="image" src="https://github.com/user-attachments/assets/ece0a03d-5599-4b97-ae1c-cdf362c19d6b" />

In the image, we can see that there is a machine that is responding to to the queries as a legitimate machine.


<img width="1265" height="277" alt="image" src="https://github.com/user-attachments/assets/8b07ac03-8507-484c-b45e-67767c2616f8" />

We can further see that this rogue machine is the one responsible for the malicious LLMNR and MDNS traffic.

---

**Q3: As part of our investigation, identifying all affected machines is essential. What is the IP address of the second machine that received poisoned responses from the rogue machine?**

To find the second machine, I searched on Wireshark for traffic that pertains the second machine


<img width="1265" height="227" alt="image" src="https://github.com/user-attachments/assets/68b17e3f-b68c-479b-be52-2f7e4fbb342d" />

With this filter I can see the second poisoned machine that received the responses.

---

**Q4: We suspect that user accounts may have been compromised. To assess this, we must determine the username associated with the compromised account. What is the username of the account that the attacker compromised?**

When filtering for traffic based on the second recipient machine, I was able to find evidence that the attacker compromised an account via SMB.

<img width="1267" height="272" alt="image" src="https://github.com/user-attachments/assets/c407f80f-a972-4771-9b61-177a1a2ec376" />

**Q5: As part of our investigation, we aim to understand the extent of the attacker’s activities. What is the hostname of the machine that the attacker accessed via SMB?**

When viewing the TCP stream of the filter listed above, I was able to find further evidence that the attacker was able to breach the user account.


<img width="1266" height="160" alt="image" src="https://github.com/user-attachments/assets/c33dcf6b-6086-4cf8-ac34-f1e922fbd4bb" />

In the screenshot, we can see the NTLM authentication, as well as the domain of the network, and the respective compromised machine via the hostname.

---
This concludes my write-up.












