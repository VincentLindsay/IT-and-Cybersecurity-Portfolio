# Overview

- This attack will be a multi-stage simulated attack that follows the MITRE ATT&CK framework TTPs of:
    - **Reconnaisance** by:
        - Network Scanning — T1595 — Attacker performs a ping sweep and full‑port Nmap scan on 172.16.50.0/24
        - Service Enumeration — T1046 — Attacker identifies Kerberos, LDAP, RDP on 172.16.50.10
    
 
    - **Credential Access** via:
        - Kerberos Username Enumeration — T1087 — Kerbrute probes valid AD usernames
        - AS‑REP Roasting — T1556.004 — Attacker requests AS‑REP tickets for accounts without preauthentication
        - Kerberoasting — T1558.003 — Attacker requests TGS tickets for SPN accounts
        - Password Cracking — T1110.002 — Hashcat cracks AS‑REP and Kerberoast hashes
        - Registry Hive Dumping — T1003.002 - Dumped SAM, SYSTEM, SECURITY hives from DC01.
    - Initial Access
        - Valid Accounts — T1078 - Successful authentication to DC01 using Bob’s cracked domain credentials.
    - **Lateral Movement** by:
        - Using Valid Accounts — T1078 — Attacker uses cracked credentials (Privileged accounts)
        - Remote Services: SMB/Service Execution — T1021.002 -CrackMapExec confirmed Bob had local admin rights on DC01 (“Pwn3d!”).
        - WMI for Remote Execution — T1047 —  WMIexec used as an alternate remote execution vector.
 
    - **Privilege Escalation**
        - Privilege Escalation via Local Admin — T1078 —  Bob’s local admin rights on DC01 allowed full SYSTEM‑level execution.
        - Service Execution for SYSTEM Shell — T1543.003  — PsExec service created and executed, yielding NT AUTHORITY\SYSTEM.
        - Create Account — T1136.001 — Attacker creates Bobby
        - Privilege Escalation via Group Membership — T1078 — Attacker adds Bobby to Domain Admins
       
 
    - **Collection**
        - File Collection — T1005 — Attacker compresses C:\Users into a ZIP archive
        - Archive Collected Data — T1074 — Attacker uses Compress‑Archive to stage data
 
    - **Exfiltration**
        - Exfiltration Over SSH — T1048.003 — Attacker uses SCP to pull ZIP file from DC
        - Exfiltration Over Network — T1041 — Outbound connection from DC to attacker machine
 
    - **Defense Impairment**
        - Clear Windows Event Logs — T1685.005 — Attacker clears Security logs using wevtutil
     
---

# Conducting the attack
- The first phase will be the conducting of Reconnaisance to verify any active machines in the network
<img width="642" height="107" alt="image" src="https://github.com/user-attachments/assets/16f85095-30c0-403f-9c3f-f1ba36357919" />

- Using fping, we can see that there is three machines active, the 172.16.50.1 IP can be seen as the default gateway.

- Next, nmap will be used to identify the open ports of 172.16.50.10
<img width="592" height="57" alt="image" src="https://github.com/user-attachments/assets/6cf060fa-f4dc-4872-ae66-948b31b4b4b8" />

- The results are as follows
<img width="1125" height="558" alt="image" src="https://github.com/user-attachments/assets/c9ad6a26-5a97-4230-ad93-63f12688df14" />

- Ports 88, 389, 445, and 3389 are open, which means the attack chain can proceed.
<img width="1041" height="277" alt="image" src="https://github.com/user-attachments/assets/a97dfe7c-3727-4a33-b8a3-bbd1207dcfb3" />

- Since we know the name of the domain: **phoenix.local**, we can proceed with enumaration of Active Directory services using kerbrute.
<img width="947" height="347" alt="image" src="https://github.com/user-attachments/assets/23f5ddc8-b5e4-414a-9366-da9f47676d2c" />

- I found 5 valid usernames using enumeration of kerberos.

- Next, I will identify which accounts do not require Kerberos authentication using the user list.
<img width="1142" height="252" alt="image" src="https://github.com/user-attachments/assets/84ec7324-9b00-4460-8443-8fd5fc790452" />

- Now the attacker will attempt to Kerberoast, however this failed, meaning the attacker will have to try a different route.
<img width="1310" height="111" alt="image" src="https://github.com/user-attachments/assets/93a7ba4e-16f6-4ccd-b606-300371be0db6" />

- The attempt at password spraying failed, so I moved onto attempting to brute force accounts
<img width="1107" height="278" alt="image" src="https://github.com/user-attachments/assets/29bbe858-593c-4cf0-9ce4-20654285adaf" />

<img width="1102" height="301" alt="image" src="https://github.com/user-attachments/assets/dbd4f77f-06e4-4fc5-9442-d9c45d191aa5" />

- Brute forcing was successful.
- With the successful brute forcing, I will attempt to connect to the machine using various remote connections.
- Using **crackmapexec**, I found that the account named **Bob** was successful for attempting to connect to via SMB.

<img width="1512" height="87" alt="image" src="https://github.com/user-attachments/assets/bc788f11-8ee0-4b85-b534-42d7e18ed96f" />

- Now the attacker has reached a pivotal point in their attack, being able to access the Domain Controller.

<img width="1612" height="121" alt="image" src="https://github.com/user-attachments/assets/e8dbee07-ddca-439a-8e43-ad347a3af956" />

- Now we will attempt to remotely access the Domain Controller.
<img width="1310" height="268" alt="image" src="https://github.com/user-attachments/assets/049c84ff-a575-4e67-a1e5-f2d0ba2a9710" />

- After sometime, I was able to crack a remote shell with psexec.exe using impacket.
<img width="1343" height="371" alt="image" src="https://github.com/user-attachments/assets/17916650-e75d-46dd-a859-5150f7ef36d3" />

- We've achieved the **SYSTEM** account access, and therefore achieved full domain compromise.
- Now the attacker will begin retrieving vital information like cached credentials in the domain.
<img width="846" height="150" alt="image" src="https://github.com/user-attachments/assets/96c23246-a5bc-48e9-a8cb-b1da074822ad" />

- In addition, a brand new Domain Account knwon as **Bobby** was created.
- The account has domain wide persistence. 
<img width="625" height="151" alt="image" src="https://github.com/user-attachments/assets/7fdf27b9-facc-4347-ba81-0bf8ee96d5b6" />

- Lastly, the attacker clears logs to hide their presence.
<img width="630" height="85" alt="image" src="https://github.com/user-attachments/assets/9ca196cb-d910-484e-a44a-2847da238c43" />


