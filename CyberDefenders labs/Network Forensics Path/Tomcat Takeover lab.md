# Tomcat Takeover Lab Write-Up [CyberDefenders]
<img width="1257" height="390" alt="image" src="https://github.com/user-attachments/assets/e4099959-bbba-41d7-a00b-7c89a85c9c92" />

lab link: https://cyberdefenders.org/blueteam-ctf-challenges/tomcat-takeover/

---
Scenario: The SOC team has identified suspicious activity on a web server within the company’s intranet. To better understand the situation, they have captured network traffic for analysis. The PCAP file may contain evidence of malicious activities that led to the compromise of the Apache Tomcat web server. Your task is to analyze the PCAP file to understand the scope of the attack

---

Q1: Given the suspicious activity detected on the web server, the PCAP file reveals a series of requests across various ports, indicating potential scanning behavior. Can you identify the source IP address responsible for initiating these requests on our server?

When viewing the PCAP, I can see that there were various conversations taken place between internal IP addresses, as well as an external IP address.

<img width="1262" height="476" alt="image" src="https://github.com/user-attachments/assets/28ee26b3-032e-4e56-b9b8-414ee1ce9871" />

We can verify the legitimacy of this conversation by filtering the specific conversation.

<img width="1265" height="626" alt="image" src="https://github.com/user-attachments/assets/73fb0dcb-dff1-4f45-90a1-057ae9d3c450" />

Based on this, we can assume that 14[.]0[.]0[.]120 is the malicious IP address.

---
Q2: Based on the identified IP address associated with the attacker, can you identify the country from which the attacker’s activities originated?

For this question, I utilized abuseipdb.com, I found that the IP address of origin is located within China.
<img width="1002" height="597" alt="image" src="https://github.com/user-attachments/assets/a0a32897-108a-45b9-ac84-45da0745b484" />

---

Q3: From the PCAP file, multiple open ports were detected as a result of the attacker’s active scan. Which of these ports provides access to the web server admin panel?
When filtering HTTP traffic, I found that there were numerous requests made between the attacker, and the webserver.
<img width="1262" height="287" alt="image" src="https://github.com/user-attachments/assets/0c4395dc-403e-4110-927c-608fc70564f4" />

We can see specific requests made by the attacker in order to attempt to gain access to an admin panel. The web server had an open port of 8080, an alternative HTTP port.
<img width="1270" height="552" alt="image" src="https://github.com/user-attachments/assets/69334784-26dc-4246-ad1c-711c61f36a8a" />

---
Q4: Following the discovery of open ports on our server, it appears that the attacker attempted to enumerate and uncover directories and files on our web server. Which tools can you identify from the analysis that assisted the attacker in this enumeration process?
We can see that the attacker enumerate several directories of the web server.
<img width="1267" height="312" alt="image" src="https://github.com/user-attachments/assets/338f7266-0beb-45c3-b4eb-2ac145ca47ab" />

The attacker utilized gobuster, to conduct the enumeration of the directories, and we can see this in the User-Agent section of the requests.

---
Q5: After the effort to enumerate directories on our web server, the attacker made numerous requests to identify administrative interfaces. Which specific directory related to the admin panel did the attacker uncover?
When analyzing the TCP stream, we can see the specific enumerated directories.
<img width="1262" height="425" alt="image" src="https://github.com/user-attachments/assets/a98d5006-1dcf-462f-b610-5d441529307b" />

The above screenshot shows a snippet of some enumeration, and what appears to be the successful enumeration of an administrative panel known as /manager/. Even though the status code is 401-Unauthorized, the attacker still knows its there.

---
Q6: After accessing the admin panel, the attacker tried to brute-force the login credentials. Can you determine the correct username and password that the attacker successfully used for login?

- When viewing the emumeration, we can see that the attacker attempted to use basic authorization.
<img width="1267" height="320" alt="image" src="https://github.com/user-attachments/assets/a0046f40-7610-4a74-bcb8-d7de294eaa09" />

Using the http.authbasic filter, we can see specific requests using this authorization.
<img width="1267" height="185" alt="image" src="https://github.com/user-attachments/assets/d423ecac-727e-4030-bbaa-b246ae801c0b" />

When viewing the POST request, we can see the credentials used to access the admin panel
<img width="1270" height="212" alt="image" src="https://github.com/user-attachments/assets/d68e6f99-a650-46d7-81ec-7179d0233939" />

---
Q7: Once inside the admin panel, the attacker attempted to upload a file with the intent of establishing a reverse shell. Can you identify the name of this malicious file from the captured data?

-In the file panel session, the attacker uploaded a file called JXQOZY.war
<img width="1002" height="102" alt="image" src="https://github.com/user-attachments/assets/8c39a6ac-fcf1-4060-9b50-6b36bbf50d02" />


After uploading the file, we can see that the attacker successfully uploaded a reverse shell.
<img width="1262" height="185" alt="image" src="https://github.com/user-attachments/assets/10e076b8-4650-44d9-8997-cd8323b2b9a1" />

We can also see that the reverse shell works via this TCP handshake.
<img width="1272" height="117" alt="image" src="https://github.com/user-attachments/assets/e5566558-88ce-4a0a-af66-2b9388cf07df" />

---
Q8: After successfully establishing a reverse shell on our server, the attacker aimed to ensure persistence on the compromised machine. From the analysis, can you determine the specific command they are scheduled to run to maintain their presence?

- We can see that the attacker made some commands that verified that the attacker had access to the root account. Additionally, we can also see that the attacker created a cronjob that actively maintains a connection with their IP via HTTPS.
<img width="1265" height="207" alt="image" src="https://github.com/user-attachments/assets/e4c51557-b2c1-4bed-acf6-79bb86b05a11" />

---
This concludes my write-up.















