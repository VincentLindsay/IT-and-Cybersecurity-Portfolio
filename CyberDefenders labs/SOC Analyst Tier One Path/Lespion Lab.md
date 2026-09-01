# Lespion Lab Write-up [CyberDefenders]

<img width="1276" height="365" alt="image" src="https://github.com/user-attachments/assets/a0acba0c-42b7-4ae6-80b1-7732c75f16d2" />
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

<img width="1267" height="227" alt="image" src="https://github.com/user-attachments/assets/7d7294b8-4094-4699-bc5e-9aae3552a911" />

When opening the Github.txt file, we are given a link to a profile. When viewing the profile, I can see various repositories, especially ones that could pertain to malicious activity (e.g mimikatz, Empire, etc.).

When viewing a repository known as Project-Build — Custom-Login-Page, I can see two javascript files.


<img width="1126" height="222" alt="image" src="https://github.com/user-attachments/assets/aafccb68-c930-410a-aa47-08c644eff5d4" />

When viewing the Login Page.js file, I can evidence of a hardcoded API key.

---

**Q2: File -> Github.txt: What plaintext password did the insider add to his GitHub repositories?**

Similar to the hardcoded API key, I can see a username and password hardcoded, however, the password was encoded in base64. I used CyberChef to decode the password, and obtain the plaintext password.


<img width="1267" height="315" alt="image" src="https://github.com/user-attachments/assets/f2c9a7ca-bcba-4b14-832b-1914bfb2ced2" />

---

**Q3: File -> Github.txt: What cryptocurrency mining tool did the insider use?**

When viewing the various repositories, I found the respective tool for mining cryptocurrency.

<img width="1242" height="217" alt="image" src="https://github.com/user-attachments/assets/6b428b5c-5298-45f8-a9a4-55b7bdc733d7" />

---
**Q4: On which gaming website did the insider have an account?**

When google searching for the username of the insider threat, I found an Instagram account known as EMarseille99, and I found a post with a QR code.


<img width="482" height="650" alt="image" src="https://github.com/user-attachments/assets/a0349d36-7b99-4544-a13d-caa92ada5168" />

This QR code takes us to the Insider’s Steam profile.

---

**Q5: What is the link to the insider Instagram profile?**

I found the full link to the insider’s Instagram profile after finding their profile on the platform.

---

**Q6: Which country did the insider visit on her holiday?**


<img width="941" height="492" alt="image" src="https://github.com/user-attachments/assets/c07f28f8-da91-4967-af0c-f1a7a990f20c" />

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




