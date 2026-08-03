# Lespion Lab Write-up [CyberDefenders]

<img width="1100" height="313" alt="image" src="https://github.com/user-attachments/assets/bc08dbaa-6369-457e-a82d-c2b2f1d70c3e" />
Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/lespion/

---

Scenario: You have been tasked by a client whose network was compromised and brought offline to investigate the incident and determine the attacker’s identity.

Incident responders and digital forensic investigators are currently on the scene and have conducted a preliminary investigation. Their findings show that the attack originated from a single user account, probably, an insider. Investigate the incident, find the insider, and uncover the attack actions.

---

Tools used:

* Google maps
* Google image search
* Sherlock

---

**Q1: File -> Github.txt: What API key did the insider add to his GitHub repositories?**

When viewing the file, I noticed there was four different files, two text files, and two image files.

<img width="1071" height="190" alt="image" src="https://github.com/user-attachments/assets/892effbe-63f4-42df-8d4c-fa212d238b17" />

When opening the Github.txt file, we are given a link to a profile. When viewing the profile, I can see various repositories, especially ones that could pertain to malicious activity (e.g mimikatz, Empire, etc.).

When viewing a repository known as Project-Build — Custom-Login-Page, I can see two javascript files.


<img width="893" height="178" alt="image" src="https://github.com/user-attachments/assets/bb2165ac-ebba-439f-902d-09e590c99fce" />

When viewing the Login Page.js file, I can evidence of a hardcoded API key.

---

**Q2: File -> Github.txt: What plaintext password did the insider add to his GitHub repositories?**

Similar to the hardcoded API key, I can see a username and password hardcoded, however, the password was encoded in base64. I used CyberChef to decode the password, and obtain the plaintext password.


<img width="1100" height="274" alt="image" src="https://github.com/user-attachments/assets/f6d41023-0e04-4a1b-af8b-6df10c0dee9e" />

---

**Q3: File -> Github.txt: What cryptocurrency mining tool did the insider use?**

When viewing the various repositories, I found the respective tool for mining cryptocurrency.

<img width="1100" height="189" alt="image" src="https://github.com/user-attachments/assets/f41703d9-3922-48f8-ba5d-378128a23098" />

---
**Q4: On which gaming website did the insider have an account?**

When google searching for the username of the insider threat, I found an Instagram account known as EMarseille99, and I found a post with a QR code.


<img width="395" height="527" alt="image" src="https://github.com/user-attachments/assets/b3e43d5e-076e-4755-9340-b1f786ce6a3d" />

This QR code takes us to the Insider’s Steam profile.

---

**Q5: What is the link to the insider Instagram profile?**

I found the full link to the insider’s Instagram profile after finding their profile on the platform.

---

**Q6: Which country did the insider visit on her holiday?**


<img width="756" height="400" alt="image" src="https://github.com/user-attachments/assets/baba3073-451a-4ad4-aaf5-1fd1b255081c" />

When using google image search on this image, I found out what country the insider threat visited on their holiday (Singapore).

---

**Q7: Which city does the insider family live in?**

Following the same process as the last question, I used google images to search for specific cities. I found that the family lives in the UAE, and they may live in Dubai.

---

**Q8: File -> office.jpg: You have been provided with a picture of the building in which the company has an office. Which city is the company located in?**

When image searching for the office, I found that the office in located in the United Kingdom.

---

**Q9: File -> Webcam.png: With the intel, you have provided, our ground surveillance unit is now overlooking the person of interest suspected address. They saw them leaving their apartment and followed them to the airport. Their plane took off and landed in another country. Our intelligence team spotted the target with this IP camera. Which state is this camera in?**


Similarly, I found that the image’s approximate location pertains to the courtyard of the University of Notre Dame, located in the state of Indiana.

---

This concludes my write-up.




