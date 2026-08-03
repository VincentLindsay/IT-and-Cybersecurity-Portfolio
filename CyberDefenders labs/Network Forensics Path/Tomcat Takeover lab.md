# Tomcat Takeover Lab Write-Up [CyberDefenders]
<img width="1257" height="422" alt="image" src="https://github.com/user-attachments/assets/558106fa-cf65-4ebb-a859-62778e277617" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/tomcat-takeover/

---
Scenario: The SOC team has identified suspicious activity on a web server within the company’s intranet. To better understand the situation, they have captured network traffic for analysis. The PCAP file may contain evidence of malicious activities that led to the compromise of the Apache Tomcat web server. Your task is to analyze the PCAP file to understand the scope of the attack

---

Q1: Given the suspicious activity detected on the web server, the PCAP file reveals a series of requests across various ports, indicating potential scanning behavior. Can you identify the source IP address responsible for initiating these requests on our server?

When viewing the PCAP, I can see that there were various conversations taken place between internal IP addresses, as well as an external IP address.

<img width="1100" height="412" alt="image" src="https://github.com/user-attachments/assets/ab9ed9f7-e6ec-412b-b232-fd922ea19c01" />

We can verify the legitimacy of this conversation by filtering the specific conversation.

<img width="1100" height="543" alt="image" src="https://github.com/user-attachments/assets/1a080c4a-3cc6-4dda-bfd8-464ccc44bc79" />

Based on this, we can assume that 14[.]0[.]0[.]120 is the malicious IP address.

---
Q2: Based on the identified IP address associated with the attacker, can you identify the country from which the attacker’s activities originated?

For this question, I utilized abuseipdb.com, I found that the IP address of origin is located within China.
<img width="813" height="487" alt="image" src="https://github.com/user-attachments/assets/7189c768-72ab-40da-97ab-789b345362b9" />

---

Q3: From the PCAP file, multiple open ports were detected as a result of the attacker’s active scan. Which of these ports provides access to the web server admin panel?
When filtering HTTP traffic, I found that there were numerous requests made between the attacker, and the webserver.
<img width="1100" height="248" alt="image" src="https://github.com/user-attachments/assets/d447f882-a874-4542-ae95-e1788aaec8f5" />
We can see specific requests made by the attacker in order to attempt to gain access to an admin panel. The web server had an open port of 8080, an alternative HTTP port.
<img width="1100" height="476" alt="image" src="https://github.com/user-attachments/assets/a1452ead-f228-45e4-81ed-f8381c49d0ec" />

---
Q4: Following the discovery of open ports on our server, it appears that the attacker attempted to enumerate and uncover directories and files on our web server. Which tools can you identify from the analysis that assisted the attacker in this enumeration process?
We can see that the attacker enumerate several directories of the web server.
<img width="1100" height="269" alt="image" src="https://github.com/user-attachments/assets/0ff4a33d-2484-48d5-81e3-d3cbfb502002" />
The attacker utilized gobuster, to conduct the enumeration of the directories, and we can see this in the User-Agent section of the requests.

---
Q5: After the effort to enumerate directories on our web server, the attacker made numerous requests to identify administrative interfaces. Which specific directory related to the admin panel did the attacker uncover?
When analyzing the TCP stream, we can see the specific enumerated directories.
<img width="1100" height="364" alt="image" src="https://github.com/user-attachments/assets/d5d0726e-52e2-4fe9-a832-69480a882ba8" />
The above screenshot shows a snippet of some enumeration, and what appears to be the successful enumeration of an administrative panel known as /manager/. Even though the status code is 401-Unauthorized, the attacker still knows its there.

---
Q6: After accessing the admin panel, the attacker tried to brute-force the login credentials. Can you determine the correct username and password that the attacker successfully used for login?
When viewing the emumeration, we can see that the attacker attempted to use basic authorization.
<img width="1100" height="270" alt="image" src="https://github.com/user-attachments/assets/e41ced05-c45a-43b3-81da-cf15e0912277" />
Using the http.authbasic filter, we can see specific requests using this authorization.
<img width="1100" height="158" alt="image" src="https://github.com/user-attachments/assets/9e2d2049-081a-4c8a-ad7f-2ca8c4bf2ecb" />
When viewing the POST request, we can see the credentials used to access the admin panel
<img width="1100" height="189" alt="image" src="https://github.com/user-attachments/assets/03b756fc-849a-4318-8a65-a9db5dd992f1" />

---
Q7: Once inside the admin panel, the attacker attempted to upload a file with the intent of establishing a reverse shell. Can you identify the name of this malicious file from the captured data?
In the file panel session, the attacker uploaded a file called JXQOZY.war
<img width="802" height="78" alt="image" src="https://github.com/user-attachments/assets/2487ccef-9cb4-41e4-999c-5a60f722a04a" />
After uploading the file, we can see that the attacker successfully uploaded a reverse shell.
<img width="1100" height="151" alt="image" src="https://github.com/user-attachments/assets/31051191-c25d-46a3-be0e-d61b577a5f03" />
We can also see that the reverse shell works via this TCP handshake.
<img width="1100" height="98" alt="image" src="https://github.com/user-attachments/assets/71eb7c7c-6031-479a-bf14-e0edea24c9f8" />

---
Q8: After successfully establishing a reverse shell on our server, the attacker aimed to ensure persistence on the compromised machine. From the analysis, can you determine the specific command they are scheduled to run to maintain their presence?
We can see that the attacker made some commands that verified that the attacker had access to the root account. Additionally, we can also see that the attacker created a cronjob that actively maintains a connection with their IP via HTTPS.
<img width="1100" height="174" alt="image" src="https://github.com/user-attachments/assets/a261075c-fb23-4226-a267-67cfe2420c18" />

---
This concludes my write-up.















