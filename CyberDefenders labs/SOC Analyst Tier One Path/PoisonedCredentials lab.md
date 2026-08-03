# PoisonedCredentials Lab Write-up [CyberDefenders]
<img width="1491" height="381" alt="image" src="https://github.com/user-attachments/assets/b5cf5e26-b10d-4d44-b018-956d6dbaea3a" />

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

<img width="1100" height="163" alt="image" src="https://github.com/user-attachments/assets/3fa624bb-0d0e-4b39-befa-db5983061076" />

Upon filtering for specific traffic using the IP address, I found interesting LLMNR queries made by the attacker.


<img width="1100" height="222" alt="image" src="https://github.com/user-attachments/assets/45eec6dd-86a4-46ab-83fe-2e0700981a71" />

I found that the attacker may have misspelled a file share name, giving their cover away while using a legitimate machine in the network.

---

**Q2: We are investigating a network security incident. To conduct a thorough investigation, We need to determine the IP address of the rogue machine. What is the IP address of the machine acting as the rogue entity?**

Since I know that the machine with the IP address 192.168.232.162 is a benign machine, I searched for conversations with this machine IP, as well as the LLMNR traffic, and additional responses.


<img width="1100" height="130" alt="image" src="https://github.com/user-attachments/assets/5620d67f-7b67-4df1-bed5-9a0f5d2badd4" />

In the image, we can see that there is a machine that is responding to to the queries as a legitimate machine.


<img width="1100" height="237" alt="image" src="https://github.com/user-attachments/assets/822adcaf-658b-4bc7-b7a2-9044c114e695" />

We can further see that this rogue machine is the one responsible for the malicious LLMNR and MDNS traffic.

---

**Q3: As part of our investigation, identifying all affected machines is essential. What is the IP address of the second machine that received poisoned responses from the rogue machine?**

To find the second machine, I searched on Wireshark for traffic that pertains the second machine


<img width="1100" height="197" alt="image" src="https://github.com/user-attachments/assets/accfda85-af2c-49ff-a635-9c4592ae9fea" />

With this filter I can see the second poisoned machine that received the responses.

---

**Q4: We suspect that user accounts may have been compromised. To assess this, we must determine the username associated with the compromised account. What is the username of the account that the attacker compromised?**

When filtering for traffic based on the second recipient machine, I was able to find evidence that the attacker compromised an account via SMB.

<img width="1100" height="233" alt="image" src="https://github.com/user-attachments/assets/5a0527e9-9b06-4bf5-bc59-2c3858d8b630" />

**Q5: As part of our investigation, we aim to understand the extent of the attacker’s activities. What is the hostname of the machine that the attacker accessed via SMB?**

When viewing the TCP stream of the filter listed above, I was able to find further evidence that the attacker was able to breach the user account.


<img width="1100" height="135" alt="image" src="https://github.com/user-attachments/assets/0be6b02d-4e2d-49d9-8720-9c4f01be38e4" />

In the screenshot, we can see the NTLM authentication, as well as the domain of the network, and the respective compromised machine via the hostname.

---
This concludes my write-up.












