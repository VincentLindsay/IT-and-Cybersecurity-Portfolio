# Overview
<img width="1647" height="390" alt="image" src="https://github.com/user-attachments/assets/33c1e9ee-c075-4f44-967e-0feb27edda6a" />

lab link:https://cyberdefenders.org/blueteam-ctf-challenges/openfire/

# Scenario
As a cybersecurity analyst, you are tasked with investigating a data breach targeting your organization’s Openfire messaging server. Attackers have exploited a vulnerability in the server, compromising sensitive communications and potentially exposing critical data. Your task is to analyze the provided network capture files using Wireshark. Identify evidence of the exploitation, trace the attacker’s actions, and uncover indicators of compromise.

# Tools used
- Wireshark



# Question 1
What is the CSRF token value for the first login request?

- To identify the CRSF token value, I searched for HTTP POST requests to find the login requests.

<img width="1911" height="192" alt="image" src="https://github.com/user-attachments/assets/0ee4ef4e-157a-46ad-9365-040bbd625439" />

- When examining the first packet of the **http.request.method == POST** filter, we can see the contents of the CSRF token

<img width="1517" height="267" alt="image" src="https://github.com/user-attachments/assets/e3a823e9-6c4a-4b7e-8541-f2417cb7b5e3" />


# Question 2
What is the password of the first user who logged in?

- When examining the first packet, we can see the login details of the user who attempted to login.
<img width="1517" height="267" alt="image" src="https://github.com/user-attachments/assets/e3a823e9-6c4a-4b7e-8541-f2417cb7b5e3" />

# Question 3
What is the 1st username that was created by the attacker?

- To find the first username that was created by the attacker, I searched for packets that contain the creation of a username.
<img width="1917" height="386" alt="image" src="https://github.com/user-attachments/assets/39d0dfe2-5df3-459e-aee8-888efbca1079" />


- Interestingly, we can see that the attacker made several requests to the **login.jsp** page.
  - When reading the TCP stream of the first GET request, we find the username that the attacker created.
<img width="1917" height="466" alt="image" src="https://github.com/user-attachments/assets/a0c74284-7841-4ce4-b3df-5b022ee653d2" />


# Question 4
What is the username that the attacker used to login to the admin panel?

- I identify the name of the user that was used to login to the admin panel, I searched for POST requests that refer to an admin panel.
<img width="1917" height="387" alt="image" src="https://github.com/user-attachments/assets/68dab17e-1c7b-4a8c-afb2-3f0d5f38d03c" />

- We can see 4 POST requests to an admin panel.
 - When examining the TCP stream, we can see the exact username that was used.
<img width="1695" height="497" alt="image" src="https://github.com/user-attachments/assets/6056f251-9705-4e1f-aa7a-61b508b055a2" />
    
# Question 5
What is the name of the plugin that the attacker uploaded?

- When checking the POST requests, we can see that there is a packet that is usually large, and worth investigating.
<img width="1917" height="342" alt="image" src="https://github.com/user-attachments/assets/7b2f954b-4ce7-4f21-9f09-0f6af6f93f2a" />

- When viewing the HTTP stream of the packet, we can see the exact POST request that indicates the uploading of a file.
<img width="1232" height="342" alt="image" src="https://github.com/user-attachments/assets/31e3c58b-dd96-45a4-9127-18f3050ea774" />

# Question 6
What is the first command that the user executed?

- In the later parts of the POST requests, we can see the use of a cmd plugin.
<img width="1935" height="398" alt="image" src="https://github.com/user-attachments/assets/737a9a6b-1d0a-4e52-a0a3-a56db29ea374" />

- When examing the contents of the first packet that contains cli usage, we can find the first command used by the attacker.
<img width="1916" height="676" alt="image" src="https://github.com/user-attachments/assets/21bb2ee4-1fa8-44c7-8ecf-4dad32355d59" />


# Question 7
Which tool did the attacker use to get a reverse shell?

- Similarly to question 6, we can see the tool the attacker used to gain reverse shell accessibility.
<img width="1917" height="672" alt="image" src="https://github.com/user-attachments/assets/5b08ea53-f6e6-4d22-9d80-c19d0081abad" />


# Question 8
Which command did the attacker execute on the server to check for network interfaces?

- To identify the attacker's traffic, I searched for the attacker's IP address, and the port used by their tool.
<img width="1917" height="492" alt="image" src="https://github.com/user-attachments/assets/094c5e9f-0518-4b30-a625-2e97a7360d03" />

- We can see some of the commands the attacker used if you follow the tcp stream.
<img width="1917" height="387" alt="image" src="https://github.com/user-attachments/assets/cebbec20-16d3-4383-b72c-231dc6983019" />

# Question 9
What is the CVE of the vulnerability exploited?

- To find the exact vulnerability, I searched for **"Openfire Plugin cve**, and found the CVE of interest.
<img width="912" height="347" alt="image" src="https://github.com/user-attachments/assets/150a3c70-ac3f-4ce4-8705-3bcf5680590b" />

# End of lab
- This concludes my write-up

- Please feel free to connect with me on linkedin: www.linkedin.com/in/vincent-lindsay







































