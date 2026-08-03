# WebStrike lab write-up [CyberDefenders]

Lab link: [https://cyberdefenders.org/blueteam-ctf-challenges/webstrike/]

---
<img width="1100" height="308" alt="image" src="https://github.com/user-attachments/assets/6469d23d-e184-44d8-aa80-db0628beb419" />

# Scenario:
A suspicious file was identified on a company web server, raising alarms within the intranet. The Development team flagged the anomaly, suspecting potential malicious activity. To address the issue, the network team captured critical network traffic and prepared a PCAP file for review.
Your task is to analyze the provided PCAP file to uncover how the file appeared and determine the extent of any unauthorized activity.

---
Tools used:

* Wireshark
* ipgeolocation.io

---
**Q1: Identifying the geographical origin of the attack facilitates the implementation of geo-blocking measures and the analysis of threat intelligence. From which city did the attack originate?**

Upon viewing the PCAP, I can see two conversations taking place amongst two different IP addresses:

<img width="1100" height="110" alt="image" src="https://github.com/user-attachments/assets/669f2f5f-7de5-4b44-8290-7186094220c0" />

Additionally, when using the **http.request** filter on Wireshark, I noticed some suspicious HTTP requests, leaving me certain the domain 117[.]11[.]88[.]124 is our bad domain.

<img width="1100" height="134" alt="image" src="https://github.com/user-attachments/assets/329ebdea-ed96-4b97-98bb-6d74eabb0b6f" />

When searching on abuseipdb.com, and on ipgeolocation.io, I found that the domain’s geolocation pertains to Tainjin, China.

---

**Q2: Knowing the attacker’s User-Agent assists in creating robust filtering rules. What’s the attacker’s Full User-Agent?**

By using the previous **http.request** filter, I was able to find the User-Agent by following the TCP string of the filtered traffic.

<img width="1045" height="147" alt="image" src="https://github.com/user-attachments/assets/fdd16d9f-d34a-474e-831f-636aaae2f907" />

---

**Q3: We need to determine if any vulnerabilities were exploited. What is the name of the malicious web shell that was successfully uploaded?**

When reviewing HTTP requests, I found several POST requests that pertained to the TA, and I found that there was a file named image.jpg.php which could be the webshell.

<img width="1100" height="328" alt="image" src="https://github.com/user-attachments/assets/a3d6df37-6421-419d-984c-068dc0c02eec" />

---
**Q4: Identifying the directory where uploaded files are stored is crucial for locating the vulnerable page and removing any malicious files. Which directory is used by the website to store the uploaded files?**

When searching for GET requests, I was able to find the respective malicious file.

<img width="1100" height="254" alt="image" src="https://github.com/user-attachments/assets/31db833e-a7a6-4a52-916f-ecd27d027907" />

Additionally, I was able to find the company stores its uploads in the **/reviews/uploads/** directory

---

**Q5: Which port, opened on the attacker’s machine, was targeted by the malicious web shell for establishing unauthorized outbound communication?**

When looking back at previous filters, and traffic, I found evidence that the attacker was utilizing netcat.

<img width="1100" height="345" alt="image" src="https://github.com/user-attachments/assets/d44cfb9c-367c-4f3c-9582-654e11e4f40c" />

I found that the attacker utilized port 8080, which is an alternative port used for HTTP.

---

**Q6: Recognizing the significance of compromised data helps prioritize incident response actions. Which file was the attacker attempting to exfiltrate?**

After looking for successful connections made through the reverse shell, I found that there was a sucessful reverse shell made by the attacker.

<img width="1100" height="29" alt="image" src="https://github.com/user-attachments/assets/68757283-af79-4fe7-845b-d23afdb100d0" />

As a result, I found further evidence that the TA was verifying the reverse shell via the use of Linux user identification commands.

<img width="1100" height="107" alt="image" src="https://github.com/user-attachments/assets/5268224c-d5dc-4d8c-a520-ecc1b8b6fb2c" />

Moreover, the attacker was attempting to retrieve the passwd file. From what I understand, the attacker was trying get a baseline of what accounts could be used to gain access.

<img width="988" height="107" alt="image" src="https://github.com/user-attachments/assets/f691918f-e4fc-468a-9e3c-a24ab0ed9b3e" />

---

This concludes my write-up. Please feel free to leave feedback, and you may connect with me on  [LinkedIn](http://www.linkedin.com/in/vincent-lindsay):








