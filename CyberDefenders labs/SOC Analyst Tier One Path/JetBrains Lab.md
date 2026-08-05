# Overview

- lab link: https://cyberdefenders.org/blueteam-ctf-challenges/jetbrains/
<img width="1638" height="522" alt="image" src="https://github.com/user-attachments/assets/766cd707-ac4c-4726-b4ab-f5af5e2c66b1" />

- Tools used:
  - Wireshark
  - NetworkMiner
  - Brim 

# Scenario:
- During a recent security incident, an attacker successfully exploited a vulnerability in our web server, allowing them to upload webshells and gain full control over the system. The attacker utilized the compromised web server as a launch point for further malicious activities, including data manipulation. 

- As part of the investigation, You are provided with a packet capture (PCAP) of the network traffic during the attack to piece together the attack timeline and identify the methods used by the attacker. The goal is to determine the initial entry point, the attacker's tools and techniques, and the compromise's extent.

# Question 1
**Identifying the attacker's IP address helps trace the source and stop further attacks. What is the attacker's IP address?**

- Prior to conducting the investigation, I added the fields of **src, and dest port** to view the source port, and destination ports used in each conversation.
<img width="691" height="495" alt="image" src="https://github.com/user-attachments/assets/6ee2bdc3-9c45-4878-9053-f59a781b4a3b" />

- When viewing the conversations, I noticed a conversation taken place between the IP address 172.17.0.2 and **23.158.56.196**, this seems to be the attacker IP address.
<img width="1624" height="677" alt="image" src="https://github.com/user-attachments/assets/90bcea8d-1d83-4180-a01d-5829213c4338" />

# Question 2 
**To identify potential vulnerability exploitation, what version of our web server service is running?**


- Since this environment pertains to a JetBrains webserver, I searched for TCP port 8111.
<img width="1918" height="948" alt="image" src="https://github.com/user-attachments/assets/47eb6502-7db0-45fb-aad8-f81735a44fc4" />
 
- I followed the TCP stream to find the web server's version.
- When sifting through the traffic, I found a conversation that involved HTTP methods like GET requests.
<img width="1918" height="937" alt="image" src="https://github.com/user-attachments/assets/8886b8a7-d4b3-4d40-9f3b-971bd7eea684" />

- When viewing the contents of a packet, I found the version by keyword search.
<img width="1366" height="940" alt="image" src="https://github.com/user-attachments/assets/9b6cdd7c-6698-47fa-aa17-4492f8735620" />

# Question 3
**After identifying the version of our web server service, what CVE number corresponds to the vulnerability the attacker exploited?**

- When conducting a web searching on the **CVE** of the Jetbrains TeamCity service I found that the **CVE** was classified as **CVE-2024-21798**.
Which was categorized as an authentication bypass vulnerability.

I found an article from Rapid7, which discusses in detail how the vulnerability can be exploited: https://www.rapid7.com/blog/post/ra-cve-2024-27198-analysis/

# Question 4 
**The attacker exploited the vulnerability to create a user account. What credentials did he set up?**

- To find the attacker's credentials, I searched for traffic associated with the IP address.
- When reading the article, it seems that the vulnerability pertains to HTTP request methods.
<img width="1912" height="947" alt="image" src="https://github.com/user-attachments/assets/fb601c55-a2c5-4b65-8416-8888651111ee" />

- I searched for POST requests based off the attacker's IP address.

<img width="1918" height="946" alt="image" src="https://github.com/user-attachments/assets/c3070e7e-d755-4231-a881-556a123ec020" />

- I also searched for POST requests containing the uri of "/users/"
- We can see that the user created an account in the **/app/rest/users** directory, that has system administrator privileges.
<img width="1286" height="932" alt="image" src="https://github.com/user-attachments/assets/b5d91d24-7b21-4433-8426-aa2a77b081f9" />

# Question 5 
**The attacker uploaded a webshell to ensure his access to the system. What is the name of the file that the attacker uploaded?**
- When searching in the previous TCP stream, I filtered the traffic through **/admin** since we know that the attacker has administrator privileges.
<img width="1242" height="410" alt="image" src="https://github.com/user-attachments/assets/d912b61b-cc58-474b-922a-65a07998aea6" />

- As a result, I was able to find the POST request pertaining to the upload of the web shell.

# Question 6 
**When did the attacker execute their first command via the web shell?**

- By searching for the file associated with the web shell, we can find the creation of a **.jsp** file, and find the time of the first executed command.
<img width="1242" height="410" alt="image" src="https://github.com/user-attachments/assets/35e5f600-ea2a-4c78-81c6-e77ae57b58d6" />

<img width="1233" height="577" alt="image" src="https://github.com/user-attachments/assets/7c491b4a-7076-4bd3-b94f-3dda5ecf50cd" />

# Question 7
**The attacker tampered with a text file that contained the credentials of the admin user of the webserver. What new username and password did the attacker write in the file?**

- To find the tampered text file, I searched for specific traffic associated with the IP address of the attacker, the .jsp file, and a POST method.


<img width="1915" height="837" alt="image" src="https://github.com/user-attachments/assets/d0c0883d-d402-44ae-81a2-72956c89f33b" />


<img width="1276" height="706" alt="image" src="https://github.com/user-attachments/assets/79a2969e-db88-4345-97eb-4a2a883d0bb5" />

- I found the tampered text file with the new credentials the attacker added.
<img width="1238" height="751" alt="image" src="https://github.com/user-attachments/assets/f53fafec-f4f7-4aff-85cb-cf1c0409de1b" />

# Question 8 
**What is the MITRE Technique ID for the attacker's action in the previous question (Q7) when tampering with the text file?**

- Since I know that the attacker added new data to a file, the Tactic would fall under Data Manipulation: T1565.001. This Technique falls under the impact tactic.

# Question 9
**The attacker tried to escape from the container but he didn’t succeed, What is the command that he used for that?**

- Using the previous filter, We can see that the attacker tried to escape the docker container.

<img width="1568" height="797" alt="image" src="https://github.com/user-attachments/assets/5e74fd45-0155-4e6e-a5e8-5bb514641eaf" />


