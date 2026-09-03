# Overview
<img width="1732" height="382" alt="image" src="https://github.com/user-attachments/assets/ba0214e0-06dd-427b-b677-4617adf36430" />
- Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/web-investigation/

# Scenario
You are a cybersecurity analyst working in the Security Operations Center (SOC) of BookWorld, an expansive online bookstore renowned for its vast selection of literature. BookWorld prides itself on providing a seamless and secure shopping experience for book enthusiasts around the globe. Recently, you've been tasked with reinforcing the company's cybersecurity posture, monitoring network traffic, and ensuring that the digital environment remains safe from threats.
Late one evening, an automated alert is triggered by an unusual spike in database queries and server resource usage, indicating potential malicious activity. This anomaly raises concerns about the integrity of BookWorld's customer data and internal systems, prompting an immediate and thorough investigation.
As the lead analyst in this case, you are required to analyze the network traffic to uncover the nature of the suspicious activity. Your objectives include identifying the attack vector, assessing the scope of any potential data breach, and determining if the attacker gained further access to BookWorld's internal systems.

# Tools used
- Wireshark
- Ipinfo
- Cyberchef


# Question 1
By knowing the attacker's IP, we can analyze all logs and actions related to that IP and determine the extent of the attack, the duration of the attack, and the techniques used. Can you provide the attacker's IP?

- When looking at the conversations in Wireshark, we can see 3 different conversations, however we can one conversation in particular that has the most amount of bytes.
  <img width="1607" height="160" alt="image" src="https://github.com/user-attachments/assets/22b776f9-902e-4e30-9e47-74acd0550877" />

- Furthermore, we can also see that the Interesting IP address also used HTTP in some of the conversations.
  - The IP address shown is likely the attacker IP address.
<img width="1437" height="217" alt="image" src="https://github.com/user-attachments/assets/b2d6712b-5afb-4a15-aae1-d38820cdcdc3" />


# Question 2 
If the geographical origin of an IP address is known to be from a region that has no business or expected traffic with our network, this can be an indicator of a targeted attack. Can you determine the origin city of the attacker?

- To identify the location of the IP address, I used IPinfo to find out the location of the IP.
<img width="1276" height="697" alt="image" src="https://github.com/user-attachments/assets/41ae021e-13b7-4638-a8f5-9f116daa0181" />

# Question 3
Identifying the exploited script allows security teams to understand exactly which vulnerability was used in the attack. This knowledge is critical for finding the appropriate patch or workaround to close the security gap and prevent future exploitation. Can you provide the vulnerable PHP script name?

- To find the **.php** script I used the filter of **http && frame contains "php" && ip.addr == <attacker IP>**
<img width="1621" height="310" alt="image" src="https://github.com/user-attachments/assets/aff7d77c-dda7-4bef-9f47-d0fa55b8caa0" />

- We can see an unusual amount of php usage.


# Question 4
Establishing the timeline of an attack, starting from the initial exploitation attempt, what is the complete request URI of the first SQLi attempt by the attacker?

- To identify the URI, I used the filter in question 3, and examined the contents of the first **.php** script.
<img width="932" height="195" alt="image" src="https://github.com/user-attachments/assets/90ad8b34-669c-47b3-9e87-48acf629531f" />

- We can see the attacker attempting to SQL inject the database.

# Question 5 
Can you provide the complete request URI that was used to read the web server's available databases?
<img width="1666" height="540" alt="image" src="https://github.com/user-attachments/assets/06e2b079-fdb2-40d9-adf1-4e86d7b7bb63" />

- By searching further for SQL injection attempts that attempt to read the data bases, I checked the **.php** requests.
- I then decoded the one of the request and found the request to read all of the available databases.
<img width="1537" height="242" alt="image" src="https://github.com/user-attachments/assets/37589622-75a7-4613-a04d-a256a4156225" />


# Question 6
Assessing the impact of the breach and data access is crucial, including the potential harm to the organization's reputation. What's the table name containing the website users data?

- When looking for traffic based on the malicious IP, I found the bookstore's database.
<img width="1665" height="467" alt="image" src="https://github.com/user-attachments/assets/a2a2be6a-0ed9-499e-939c-d727b43a4289" />

- I then used this database as a filter, to find the customer's data.
<img width="955" height="666" alt="image" src="https://github.com/user-attachments/assets/81c5de14-1f58-499e-915c-9d61cec9c880" />

- When viewing the traffic for one of the SQL injections, we can see the search for the bookstore's database, along with the specific table associated with the users.

# Question 7
The website directories hidden from the public could serve as an unauthorized access point or contain sensitive functionalities not intended for public access. Can you provide the name of the directory discovered by the attacker?

- To find the directory of intrest, I filtered for POST requests using the attacker IP address.
<img width="1667" height="140" alt="image" src="https://github.com/user-attachments/assets/5027c276-b0e2-49cf-9f7f-ed6c6129ac49" />

- We can see the directory that shouldn't be accessed.

# Question 8 
Knowing which credentials were used allows us to determine the extent of account compromise. What are the credentials used by the attacker for logging in?

<img width="1662" height="142" alt="image" src="https://github.com/user-attachments/assets/4b23d1aa-b677-4ca0-b91c-d404ded27998" />

<img width="1640" height="552" alt="image" src="https://github.com/user-attachments/assets/7464806f-6817-490a-a37c-fdd39cc481d7" />

- I found a series of four login attempt packets. Out of these, three packets contained invalid username and password combinations.
- One of them contained the correct login information.


# Question 9 
We need to determine if the attacker gained further access or control of our web server. What's the name of the malicious script uploaded by the attacker?

- When looking at the POST requests, we can see that one of the packets is larger in sieze, which could indicate the uploading of a file.
<img width="1662" height="142" alt="image" src="https://github.com/user-attachments/assets/eed63a90-20c4-47b5-b629-fe13836b06a2" />

- When reading the http stream of the packet, we can see the file that the attacker uploaded.
<img width="1202" height="437" alt="image" src="https://github.com/user-attachments/assets/6244e863-e066-4327-bf7a-a16d527df5a5" />
























































