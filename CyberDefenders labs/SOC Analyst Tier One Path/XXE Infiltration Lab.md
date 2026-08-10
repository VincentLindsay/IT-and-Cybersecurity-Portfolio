# Overview
lab link: https://cyberdefenders.org/blueteam-ctf-challenges/xxe-infiltration/
<img width="1288" height="382" alt="image" src="https://github.com/user-attachments/assets/37b7796a-88cf-4163-805d-a4772ab61b87" />

# Scenario
An automated alert has detected unusual XML data being processed by the server, which suggests a potential XXE (XML External Entity) Injection attack. This raises concerns about the integrity of the company's customer data and internal systems, prompting an immediate investigation.

Analyze the provided PCAP file using the network analysis tools available to you. Your goal is to identify how the attacker gained access and what actions they took.

# Tools Used
- Wireshark

# Question 1
**Identifying the open ports discovered by an attacker helps us understand which services are exposed and potentially vulnerable. Can you identify the highest-numbered port that is open on the victim's web server?**

- In this lab, we will be analyzing a PCAP file.

 - To identify the port that was vulnerable, I checked the protocol hierarchy. 
<img width="1918" height="842" alt="image" src="https://github.com/user-attachments/assets/f51ab29d-3fec-4eab-93f2-607ee0f7afe6" />

- I also checked the conversations taken place in the PCAP, and also found that there was numerous HTTP conversations, as well as a MYSQL (3306) connection.
<img width="1915" height="726" alt="image" src="https://github.com/user-attachments/assets/7c2e9907-4a38-4d1f-a15f-44255c1b109c" />

# Question 2
**By identifying the vulnerable PHP script, security teams can directly address and mitigate the vulnerability. What's the complete URI of the PHP script vulnerable to XXE Injection?**

- To find the uri, I used the filter: **http.request.uri contains "php" and http.request.method == "POST"** which checks for POST requests that could involve the PHP script.

<img width="1918" height="532" alt="image" src="https://github.com/user-attachments/assets/9e9f49cf-a7fc-4e69-8071-82c93d88b28f" />

- Furthermore, you can see the URI that the PHP script is vulnerable towards XXE injection.

# Question 3
**To construct the attack timeline and determine the initial point of compromise. What's the name of the first malicious XML file uploaded by the attacker?**

- To identify the malicious **XML**, I used the previous filter: **http.request.uri contains "php" and http.request.method == "POST"** and examined the HTTP stream of the first packet.
  <img width="1918" height="640" alt="image" src="https://github.com/user-attachments/assets/094c6033-708c-42b6-a397-d24dff8e136d" />

- We can see that each packet has the URI of interest.
  - Furthermore, the HTTP stream shows in full detail the injection of the XML file.

<img width="1285" height="932" alt="image" src="https://github.com/user-attachments/assets/e387389c-479a-42fd-bb64-84b2ac7a6415" />

# Question 4
**Understanding which sensitive files were accessed helps evaluate the breach's potential impact. What's the name of the web app configuration file the attacker read?**

- To find the exact configuration file, I checked each packet from the previous file, and found a packet containing the configuration file.
<img width="1273" height="905" alt="image" src="https://github.com/user-attachments/assets/79adea2a-aeed-43dd-b3c4-e5b041f9dd9b" />

# Question 5
**To assess the scope of the breach, what is the password for the compromised database user?**

- Similar to question 4, I examined the HTTP stream of the packet containing the server's reply to the attacker
<img width="1293" height="933" alt="image" src="https://github.com/user-attachments/assets/9119adca-0584-4d42-bd05-6ffe15794612" />

- As a result, the attacker began to access the SQL server.

# Question 6
**Following the database user compromise. What is the timestamp of the attacker's initial connection to the MySQL server using the compromised credentials after the exposure?**

- To identify the intial connection towards the MySQL server, I used the filter: **mysql**
<img width="1918" height="947" alt="image" src="https://github.com/user-attachments/assets/5a938364-5f82-4600-a8ca-e1f4d35b6f60" />

- We can see that the attacker attempted to login to the server multiple times, but they were successful.

# Question 7
**To eliminate the threat and prevent further unauthorized access, can you identify the name of the web shell that the attacker uploaded for remote code execution and persistence?**

- Using the previous filter: **http.request.uri contains "php" and http.request.method == "POST"**, I checked the details of the last packet with the URI of upload.php.

<img width="1290" height="940" alt="image" src="https://github.com/user-attachments/assets/a21ee7ba-24d3-4bee-affe-0a2922c0da18" />

- We can see that the attacker uploaded another  **XML** file that contains the web shell that contacts the C2 server.









