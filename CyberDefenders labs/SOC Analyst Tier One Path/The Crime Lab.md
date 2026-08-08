# Overview

- Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/the-crime/
<img width="1657" height="423" alt="image" src="https://github.com/user-attachments/assets/16b547d1-239d-4542-ba6d-827d66f2654b" />

# Scenario
- We're currently in the midst of a murder investigation, and we've obtained the victim's phone as a key piece of evidence. After conducting interviews with witnesses and those in the victim's inner circle, your objective is to meticulously analyze the information we've gathered and diligently trace the evidence to piece together the sequence of events leading up to the incident.

# Tools Used
- ALEAPP

# Question 1:
**Based on the accounts of the witnesses and individuals close to the victim, it has become clear that the victim was interested in trading. This has led him to invest all of his money and acquire debt. Can you identify the SHA256 of the trading application the victim primarily used on his phone?**
- In this lab, we are given the Android phone's files.
- To find the file hash of the trading application, I used ALEAPP, an Android parser, to find the file hash of the Olympic trading program.

<img width="1130" height="812" alt="image" src="https://github.com/user-attachments/assets/23da3eca-6743-4fc8-a074-89a39c94cf63" />

- I processed the entire phone's filesystem.
- As a result, I was able to extract the SHA-256 hash of the trading application.

<img width="1918" height="788" alt="image" src="https://github.com/user-attachments/assets/861b8ce1-d0cb-411b-95bd-2ad492b5dffe" />

# Question 2:
**According to the testimony of the victim's best friend, he said, "While we were together, my friend got several calls he avoided. He said he owed the caller a lot of money but couldn't repay now". How much does the victim owe this person?**

- To find the amount of money that the victim owed, I checked the SMS messages report that ALEAPP generated.
<img width="1918" height="942" alt="image" src="https://github.com/user-attachments/assets/0ff012b7-3e10-47ef-9cd5-cb6bde29f202" />

- I found a text message discussing that the victim owed the adversary 250,000 EGP.

# Question 3:
**What is the name of the person to whom the victim owes money?**

- To identify the name of the person who the victim owes money to, I checked for any report containing the phone number associated with the SMS message.
- By searching the Victim's contacts, and cross-referencing the phone number, I can see that the name of the person is: Shady Wahab
<img width="1918" height="948" alt="image" src="https://github.com/user-attachments/assets/651533f2-82e3-456c-96f7-299563a6eb7d" />

# Question 4:
**Based on the statement from the victim's family, they said that on September 20, 2023, he departed from his residence without informing anyone of his destination. Where was the victim located at that moment?**

- To identify the victim's location, I searched for logs with the date of 09/30/2023, and found several images.
<img width="1918" height="1010" alt="image" src="https://github.com/user-attachments/assets/a8c13220-e7fd-4ec6-8a4c-c3cda071972f" />

- One of the images is a google maps location of where the victim was last located.
<img width="778" height="602" alt="image" src="https://github.com/user-attachments/assets/02a4f872-6f87-4167-9b5f-ca758df00f7a" />

# Question 5
**The detective continued his investigation by questioning the hotel lobby. She informed him that the victim had reserved the room for 10 days and had a flight scheduled thereafter. The investigator believes that the victim may have stored his ticket information on his phone. Look for where the victim intended to travel.**

- When looking for anything pertaining to a plane flight, I found discord chats pertaining to a plane flight.
<img width="1918" height="765" alt="image" src="https://github.com/user-attachments/assets/6277a931-d4a4-4183-bb72-311aef05a402" />

- We can the mention of a flight to visit a place called "The Mob Museum"
<img width="1587" height="805" alt="image" src="https://github.com/user-attachments/assets/812e0e27-eb1a-4433-a362-d02ae99d1334" />

- When conducting a google search, I found that the Mob Museum was located in Las Vegas, Nevada.
<img width="1547" height="1027" alt="image" src="https://github.com/user-attachments/assets/32e27670-ab30-4ff7-b855-e4849efdcc5b" />

# Question 6
**After examining the victim's Discord conversations, we discovered he had arranged to meet a friend at a specific location. Can you determine where this meeting was supposed to occur?**
- By looking at the discord chat screenshot above, we can see that the victim was supposed to meet a friend at The Mob Museum.













