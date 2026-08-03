# Overview
- This section involves the installation of several tools to conduct the simulated attack.

# Configuring the attacker machine
- The the following table shows the attacker's toolkit, mapped by the MITRE ATT&CK framework.


| Category                     | Tools                                                                 | MITRE ATT&CK Technique – ID                                      |
|------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------|
| Reconnaissance               | Nmap, Netcat, DNSutils                                                | Active Scanning — T1595<br>Network Service Scanning — T1046<br>DNS Enumeration — T1590.004 |
| Active Directory Enumeration | Kerbrute, ldap-utils,                         | Account Discovery — T1087<br>Remote System Discovery — T1018<br>Permission Groups Discovery — T1069<br>Domain Trust Discovery — T1482 |
| Credential Access            | Impacket (GetNPUsers, GetUserSPNs), Hashcat, Responder                | AS‑REP Roasting — T1556.004<br>Kerberoasting — T1558.003<br>Password Cracking — T1110.002<br>LLMNR/NBT‑NS Poisoning — T1557.001 |
| Lateral Movement             | xfreerdp (RDP), SSH                                                   | Remote Services (RDP) — T1021.001<br>Remote Services (SSH) — T1021.004<br>Valid Accounts — T1078 |
| Privilege Escalation         | net user / net group                                                  | Create Account — T1136.001<br>Privilege Escalation via Valid Accounts — T1078 |
| Defense Evasion              | Registry modification, SharpHound, Responder                          | Modify Registry — T1112<br>Obfuscated/Encrypted Payloads — T1027<br>Spoofing — T1557 |
| Collection                   | zip/7zip                                                              | Archive Collected Data — T1074<br>File Collection — T1005 |
| Exfiltration                 | SCP/OpenSSH, curl, wget                                                | Exfiltration Over SSH — T1048.003<br>Exfiltration Over Web — T1041 |
| Command & Control            | Netcat, SSH                                                            | Unencrypted C2 — T1095<br>Encrypted C2 — T1573 |

- I will show how I configured the tools for the attack simulation.
- Since I am using a kali machine for the simulated attack, the only tools that are needed to be installed are:
-   kerbrute.

- To install kerbrute, I searched on google for: Install kerbrute
<img width="1896" height="368" alt="image" src="https://github.com/user-attachments/assets/268168ec-f361-4dbc-911a-3455748392e0" />

- I used the **kerbrute_linux_amd64** file for this installation.
- I enabled the ability for the problem to have execute permissions.
<img width="716" height="666" alt="image" src="https://github.com/user-attachments/assets/0cc66859-8ba6-40a7-a102-f0ea9e969c14" />

- I changed the name of the file to **kerbrute** to maintain simiplicity of execution. 
 <img width="637" height="192" alt="image" src="https://github.com/user-attachments/assets/09557c07-605b-4816-9557-58487b960c94" />

  

- I also moved the file to the **/usr/local/bin** directory.
<img width="627" height="48" alt="image" src="https://github.com/user-attachments/assets/a0e4a2bb-ff31-40fb-bda4-3ce48b7911d2" />

- Additionally, I also created a directory known as **phoenix_lab**, where I created a wordlist of users
<img width="637" height="382" alt="image" src="https://github.com/user-attachments/assets/372fa174-b839-4daf-8c6e-8e4d5afe24a2" />



