# Overview
Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/packetdetective/
<img width="1917" height="390" alt="image" src="https://github.com/user-attachments/assets/ccdf5566-66fc-4525-b80d-a7454e4c950a" />

# Scenario
In September 2020, your SOC detected suspicious activity from a user device, flagged by unusual SMB protocol usage. Initial analysis indicates a possible compromise of a privileged account and remote access tool usage by an attacker.

Your task is to examine network traffic in the provided PCAP files to identify key indicators of compromise (IOCs) and gain insights into the attacker’s methods, persistence tactics, and goals. Construct a timeline to better understand the progression of the attack by addressing the following questions.
# Tools Used
- Wireshark


# File's Overview
- In this lab we are given 3 different **.pcaps**, and I will mat this write-up based on the files, as well as the Questions.

#  Traffic-1.pcapng Question 1
The attacker’s activity showed extensive SMB protocol usage, indicating a potential pattern of significant data transfer or file access.
What is the total number of bytes of the SMB protocol?

- To Identify the amount of bytes taken place by the attacker's SMB usage, I checked the protocol Hierarchy
<img width="1917" height="907" alt="image" src="https://github.com/user-attachments/assets/1f6fa822-1f46-40ad-9487-e116deae6e38" />

- We can see that the number of bytes detected was 4406.

#  Traffic-1.pcapng Question 2
Authentication through SMB was a critical step in gaining access to the targeted system. Identifying the username used for this authentication will help determine if a privileged account was compromised.
Which username was utilized for authentication via SMB?

- To identify the username used in the NTLM Authentication, I used the filter **"ntlmssp"**, to identify any authentication attempts.
<img width="1917" height="541" alt="image" src="https://github.com/user-attachments/assets/164bf7ee-d8b5-418c-9d77-6d530bb92a79" />

- I found that the attacker successfully authenticated into the **Administrator** account.

#  Traffic-1.pcapng Question 3
During the attack, the adversary accessed certain files. Identifying which files were accessed can reveal the attacker's intent.
What is the name of the file that was opened by the attacker?

- I used a filter of **"smb.access.read"** to identify any SMB read requests by the attacker.
<img width="1917" height="387" alt="image" src="https://github.com/user-attachments/assets/f9739d8f-30a0-4394-b861-a9ffe0161844" />

- We can see that the attacker was reading the **eventlog** file.

# Traffic-1.pcapng Question 4
Clearing event logs is a common tactic to hide malicious actions and evade detection. Pinpointing the timestamp of this action is essential for building a timeline of the attacker’s behavior.
What is the timestamp of the attempt to clear the event log? (24-hour UTC format)

- By looking at the same packet as question 3, we can see the time that the attacker attempted to delete the logs.
<img width="1917" height="395" alt="image" src="https://github.com/user-attachments/assets/b7e269eb-fee4-42db-bce2-d7b0ce30e6b6" />

# Traffic-2.pcapng Question 1
The attacker used "named pipes" for communication, suggesting they may have utilized Remote Procedure Calls (RPC) for lateral movement across the network. RPC allows one program to request services from another remotely, which could grant the attacker unauthorized access or control.
What is the name of the service that communicated using this named pipe?

- To identify any RPC traffic, I filtered for TCP port 135, which pertains to RPC Endpoint calls.
<img width="1918" height="825" alt="image" src="https://github.com/user-attachments/assets/1c60fc75-db59-4668-9083-4c768376ac78" />

- In the packet details we can see the service the attacker used.

# Traffic-2.pcapng Question 2
Measuring the duration of suspicious communication can reveal how long the attacker maintained unauthorized access, providing insights into the scope and persistence of the attack.
What was the duration of communication between the identified addresses 172.16.66.1 and 172.16.66.36?

- To identify how long the communication took place, I checked the conversation section on Wireshark.
<img width="1917" height="741" alt="image" src="https://github.com/user-attachments/assets/93def803-a5ed-4e7a-9d34-9663028fd5aa" />

- We can see the amount of time the conversation took place.

# Traffic-3.pcapng Question 1
The attacker used a non-standard username to set up requests, indicating an attempt to maintain covert access. Identifying this username is essential for understanding how persistence was established.
Which username was used to set up these potentially suspicious requests?

- Upon opening the **pcap** file, we can see the SMB Session Request to create an account.
<img width="1917" height="627" alt="image" src="https://github.com/user-attachments/assets/070a6bd3-e5a3-4634-b465-23d955b15865" />

# Traffic-3.pcapng Question 2
The attacker leveraged a specific executable file to execute processes remotely on the compromised system. Recognizing this file name can assist in pinpointing the tools used in the attack.
What is the name of the executable file utilized to execute processes remotely?

- We can see the file that the attacker utilized.
<img width="1915" height="537" alt="image" src="https://github.com/user-attachments/assets/0a9c8427-a5b1-43f9-9c90-48801353495a" />




