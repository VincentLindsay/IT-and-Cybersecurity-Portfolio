# Overview
lab link: https://cyberdefenders.org/blueteam-ctf-challenges/awsraid/
<img width="1915" height="440" alt="image" src="https://github.com/user-attachments/assets/b3cff66b-430c-4b03-b6ae-a9f02b508c55" />

# Tools used
- Splunk

# Scenario
- Your organization utilizes AWS to host critical data and applications. An incident has been reported that involves unauthorized access to data and potential exfiltration.
  The security team has detected unusual activities and needs to investigate the incident to determine the scope of the attack.


# Question 1
- Knowing which user account was compromised is essential for understanding the attacker's initial entry point into the environment.
What is the username of the compromised user?

- To search for the compromised account, I searched via the index=aws_cloudtrail
- When looking at the **userIdentity.userName** field, we can find interesting events pertaining to the top 10 accounts.
<img width="1905" height="750" alt="image" src="https://github.com/user-attachments/assets/4916d647-95b9-45c1-b86c-ce35a278a6ac" />

- I added an additional field to my search: eventSource="signin.amazonaws.com"
- By searching for failed authentications I found 9 events
<img width="1916" height="937" alt="image" src="https://github.com/user-attachments/assets/9ccda0dd-2638-479a-b5cd-3034d80f599f" />

Query: index="aws_cloudtrail" eventSource="signin.amazonaws.com" "responseElements.ConsoleLogin"=Failure

<img width="1918" height="940" alt="image" src="https://github.com/user-attachments/assets/34d0c37e-3df2-4281-8843-6ff4dfa0c066" />
- We can see the various failed logins by the users, and the source IP address.

```Bash
Query: index="aws_cloudtrail" eventSource="signin.amazonaws.com" "responseElements.ConsoleLogin"=Failure
| stats count by sourceIPAddress, userIdentity.userName
```
<img width="1918" height="937" alt="image" src="https://github.com/user-attachments/assets/1c2b3a4e-56d9-4e03-83a0-0f8811992c48" />

- By searching for Successful authentications, I found that the **helpdesk.luke** account was compromised based on the source IP address

```Bash
Query: index="aws_cloudtrail" eventSource="signin.amazonaws.com"   "responseElements.ConsoleLogin"=Success  sourceIPAddress="185.192.70.84" 
| stats  count by _time, sourceIPAddress, userIdentity.userName
```
# Question 2
We must investigate the events following the initial compromise to understand the attacker's motives. What is the timestamp for the first access to an S3 object by the attacker?

- Now that I know what account was compromised and the source IP address to be the attacker's IP, I can cross-reference additional searches.
- I searched for events relating to S3
<img width="1918" height="947" alt="image" src="https://github.com/user-attachments/assets/7ca7a58f-128c-42f7-9407-97f618e97e15" />

- I searched for "GetObject" events, which involves the user retrieving something.
<img width="1918" height="983" alt="image" src="https://github.com/user-attachments/assets/49e3ecb6-cb33-451f-9c03-ea33f64fcf67" />

- By searching for the "GetObject" eventName, I found the exact time to the attacker's first access to an S3 object.
<img width="1915" height="938" alt="image" src="https://github.com/user-attachments/assets/69ec7008-8a1a-495f-bcfe-eb50327ee7e3" />

# Question 3
Among the S3 buckets accessed by the attacker, one contains a DWG file. What is the name of this bucket?

- By searching for **.dwg** files, I can find the name of the bucket.
<img width="1918" height="940" alt="image" src="https://github.com/user-attachments/assets/cf7aa338-741b-458e-9e35-649a3d10790b" />

- By expanding out the vent, I found the name of the S3 bucket.
<img width="1198" height="389" alt="image" src="https://github.com/user-attachments/assets/d294c5c3-bce8-44be-95aa-9001dbf3d696" />

# Question 4
We've identified changes to a bucket's configuration that allowed public access, a significant security concern. What is the name of this particular S3 bucket?

- By searching for changes to the S3 bucket's configuration, I was able to verify that the bucket configurations were changed.
<img width="1913" height="742" alt="image" src="https://github.com/user-attachments/assets/4c96cfce-8e67-4daa-9405-1910f00baefb" />

```Bash
index="aws_cloudtrail" "userIdentity.userName"="helpdesk.luke" eventSource="s3.amazonaws.com" eventName="PutBucketPublicAccessBlock"
```
<img width="1237" height="127" alt="image" src="https://github.com/user-attachments/assets/1bfbcc7c-3e45-4a22-8768-f06ac27b1dca" />

- I was able to find the bucket name.

# Question 5
Creating a new user account is a common tactic attackers use to establish persistence in a compromised environment. 
What is the username of the account created by the attacker?

- By searching for created users by the eventCategory of management, I found what account the attacker created.
<img width="1918" height="417" alt="image" src="https://github.com/user-attachments/assets/a93dbe6a-880c-42cc-af06-c7cd77b41c52" />

Query:
```Bash
index="aws_cloudtrail" eventSource="iam.amazonaws.com"  eventCategory="Management"
| search eventName="CreateUser"
| stats count by _time, userIdentity.userName
```

# Question 6: 
Following account creation, the attacker added the account to a specific group. What is the name of the group to which the account was added?

- By searching for eventName=AddUserToGroup, I was able to find that the attacker's account was added to the admins group
```Bash
index="aws_cloudtrail" eventName="AddUserToGroup"
```
<img width="1048" height="225" alt="image" src="https://github.com/user-attachments/assets/ed72dd4a-0d33-4436-8e29-b83426c2179d" />

