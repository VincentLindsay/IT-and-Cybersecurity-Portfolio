# Overview
- lab link: https://cyberdefenders.org/blueteam-ctf-challenges/grabthephisher/
<img width="1918" height="920" alt="image" src="https://github.com/user-attachments/assets/7bf39d5c-f7d3-48af-a189-4ca3628958f3" />

# Scenario
- A decentralized finance (DeFi) platform recently reported multiple user complaints about unauthorized fund withdrawals. A forensic review uncovered a phishing site impersonating the legitimate PancakeSwap exchange, luring victims into entering their wallet seed phrases. 
The phishing kit was hosted on a compromised server and exfiltrated credentials via a Telegram bot.

- Your task is to conduct threat intelligence analysis on the phishing infrastructure, identify indicators of compromise (IoCs), and track the attacker’s online presence, including aliases and Telegram identifiers, to understand their tactics, techniques, and procedures (TTPs).

# Tools Used
- Notepad++ 

# Question 1
**Which wallet is used for asking the seed phrase?**

- In this lab, I was given a zipped file.
- Upon accessing the folder, I can see that the folder's name is **pankewk** which could be Impersonating the PancakeSwap platform.
- When looking at the folder's contents, I can see the name of the Crypto wallet. 
<img width="956" height="557" alt="image" src="https://github.com/user-attachments/assets/5672647c-82f4-4860-a5bc-c3a7a149a8c8" />

# Question 2
**What is the file name that has the code for the phishing kit?**

- When looking at the contents of the wallet's folder, I was able to find the phishing kit.
<img width="992" height="202" alt="image" src="https://github.com/user-attachments/assets/bb04ac0f-c7b3-4316-a799-2f26130028cf" />

# Question 3
**In which language was the kit written?**

- You can find this via looking at the file in a notepad or other editor.
<img width="992" height="202" alt="image" src="https://github.com/user-attachments/assets/baa2176e-af80-4f1d-bda2-31c361e0ef1a" />

# Question 4
**What service does the kit use to retrieve the victim's machine information?**

- To identify the service, I looked at the contents of the file, and found a request to sypexgeo.
- Sypexgeo is a IP geolocation service.
<img width="1918" height="1038" alt="image" src="https://github.com/user-attachments/assets/cd3b0c29-41bf-4cd6-93c0-59557f831342" />

- So the service used was **sypex geo** for the retrieval of machine information.

# Question 5
**How many seed phrases were already collected?**

- When looking at the contents of the original kit, there was a log file.
<img width="952" height="993" alt="image" src="https://github.com/user-attachments/assets/4a23f891-2a77-4bb8-8ea4-a4936a1fc10c" />

- Each line of words is a seed phrase to access the user's wallet.
- So we know that the attacker collected 3 seed phrases.


# Question 6
**Could you please provide the seed phrase associated with the most recent phishing incident?**

- When reviewing the previous log file, I found the most recent seed phrase.
<img width="952" height="993" alt="image" src="https://github.com/user-attachments/assets/59301659-562c-4731-898b-855d21fbf624" />
  
# Question 7
**Which medium was used for credential dumping?**

- When looking at the **php** file you can see that the kit uses **telegram** for credential dumping.
<img width="880" height="758" alt="image" src="https://github.com/user-attachments/assets/96e4b814-3936-4cd0-a4dd-c0a3a1ebc407" />

# Question 8
**What is the token for accessing the channel?**

- Similarly, the **php** file gives additional details like the channel's token.
- The variable **$token** shows the telegram channel's token. 

<img width="852" height="312" alt="image" src="https://github.com/user-attachments/assets/44596b04-bfda-47d1-a2ea-9bc17a698db3" />

# Question 9
**What is the Chat ID for the phisher's channel?**

- In the variable **$id**, you can see the ID for the phisher's telegram channel.
<img width="1142" height="288" alt="image" src="https://github.com/user-attachments/assets/7e1cd413-f96f-4a6f-8c87-c05572d3df7c" />

# Question 10
**What are the allies of the phish kit developer?**

- To find the alias of the phish kit developer, I looked at the malicious file, and looked for comments, or any phrase.
<img width="897" height="466" alt="image" src="https://github.com/user-attachments/assets/8de8eff9-961c-4dd9-a005-812d3ac1d22c" />

- You can see that the Phisher left a comment describing the file as a gift to other threat actors, with their alias.





