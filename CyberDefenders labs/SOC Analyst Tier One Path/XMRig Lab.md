# Overview
- Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/xmrig/
<img width="1901" height="427" alt="image" src="https://github.com/user-attachments/assets/be3eba9f-b894-4ace-b5e8-1d9e15eb3200" />

# Scenario
During routine security audits at a startup, the SOC team detected unusual activity on Linux servers in the company’s infrastructure, including unexpected configuration changes and unfamiliar files in critical system directories. These anomalies suggest possible unauthorized access and raise concerns about the integrity of the server environment.

You received a disk image from one of the affected servers for forensic analysis. Your objective is to determine if a compromise has occurred, identify any tactics or tools used by a potential attacker, assess the scope and impact of the incident, and recommend mitigation strategies to safeguard against future breaches.

# Tools used

# Question 1
Assigning high-level privileges to a new user is essential in the attack chain, as it enables the attacker to execute commands with administrative access, ensuring persistent control over the system. What command did the attacker use to grant elevated privileges to the newly created user?

- To be able to analyze the image, I used the following commands:
<img width="1918" height="362" alt="image" src="https://github.com/user-attachments/assets/20a1dec6-a5d1-43ca-be7c-560180140bb3" />

- These commands assign the disk image to the loop device, and lists the loop devices.

- I mounted the 2nd partition to a new created directory called **xmrig** and began to analyze the image.

<img width="1918" height="663" alt="image" src="https://github.com/user-attachments/assets/b9ea4ef6-c1a6-4ead-b0c8-302f87d4bc89" />

- Upon checking the **home** directory, I found a user named noah.
<img width="1066" height="53" alt="image" src="https://github.com/user-attachments/assets/b978bc62-cba2-43ce-a853-cf1a7fa00af3" />

- I also reviewed the contents of the ubuntu user account, and found evidence of the noah's account creation with sudo permissions.
<img width="1313" height="147" alt="image" src="https://github.com/user-attachments/assets/bd839036-531a-465d-af63-55b30f2bfe4f" />

- We can see the account's creation, and elevation of privileges, as well as the deletion of log files.

# Question 2
Understanding the commands used by the attacker to cover their traces is essential for identifying attempts to hide malicious activity on the system. What is the second command the attacker used to erase evidence from the system?

- By reviewing the **.bash_history** logs of the **ubuntu** account, we can see that the attacker has deleted authentication logs.
<img width="1163" height="407" alt="image" src="https://github.com/user-attachments/assets/6ad4a2d8-54a8-42b2-98fb-7e19a2111d7a" />

# Question 3
Identifying the configuration added or modified by the attacker for persistence is essential for detecting and removing recurring malicious activities on the system. What configuration line did the attacker add to one of the key Linux system files for scheduled tasks to ensure the miner would run continuously?

- To identify any scheduled jobs, I need to check the addition of any cron jobs added to the server.

<img width="906" height="142" alt="image" src="https://github.com/user-attachments/assets/bad9a61a-d73a-4326-ac34-e962c49ce040" />

- I navigated to the /var/spool/cron/crontabs/root directory, and listed the contents of the cronjobs.
<img width="1277" height="708" alt="image" src="https://github.com/user-attachments/assets/a3833d5d-f2ac-43f7-a883-04cb103e03c7" />

- We can see the attacker created a new job, and we can also see the location of the file associated with the newly created job.

# Question 4
Identifying the hash of the malicious file is crucial for confirming its uniqueness and tracking its presence across systems. What is the MD5 hash of the file dropped by the attacker with mining capabilities?

- To get the file hash, I navigated to the **tmp** directory to find the file that created the cron job.
<img width="1512" height="162" alt="image" src="https://github.com/user-attachments/assets/f932e2d9-d1c8-464e-a90e-8d3420414cb4" />

- By using the **md5sum** command, I was able to obtain the hash of the file.
<img width="1918" height="243" alt="image" src="https://github.com/user-attachments/assets/4298d72e-35f8-4fa9-9a08-28cf57936a3b" />

# Question 5
Knowing the original name of a malicious file helps link it to known malware families and provides valuable insights into its behavior. According to threat intelligence reports, what is the original name of the miner?

- I used VT with the file hash to identify the file's original name.
  - By checking the details, I found the original name. 
<img width="1918" height="995" alt="image" src="https://github.com/user-attachments/assets/83c214d6-f9a1-4f79-b641-c96b19fef167" />

# Question 6 
Understanding the attacker's actions is crucial for tracing how malicious files were introduced to the system. The attacker successfully executed a command to download and save the miner on the compromised Linux system. What was the exact file path on the attacker's server where the malicious miner was hosted?

- To find the command, I used photorec to create an image of the original disk image given.
<img width="1918" height="567" alt="image" src="https://github.com/user-attachments/assets/4f19674e-fa15-4273-9d9a-c159144c88f1" />


- Once the recovery image was created, I used grep to find the **backup.elf** file.
<img width="1918" height="352" alt="image" src="https://github.com/user-attachments/assets/4996a33a-8d32-4cc7-a073-8e88313949b8" />

<img width="1275" height="618" alt="image" src="https://github.com/user-attachments/assets/b71bae7c-81e7-4978-8266-782557928e10" />

- We can see the attacker retrieving the file via a C2 server.

# Question 7

To understand which sensitive information was accessed and transferred from the compromised system, it’s essential to identify the files exfiltrated by the attacker. What is the full path on the attacker’s remote machine where the exfiltrated passwd file was saved?

- We can see the file path where the attacker saved the **passwd** file.
<img width="1229" height="576" alt="image" src="https://github.com/user-attachments/assets/65a9359a-27eb-4d3a-823a-0d9d7de5487e" />

# Question 8
Understanding how the attacker maintained elevated privileges without repeated permission prompts is essential for uncovering their methods of persistent access. What command did the attacker use to configure continuous privilege escalation without requiring repeated permission?

- We can also see that the attacker maintained privileges by adding themselves to the sudoers group.
<img width="1273" height="562" alt="image" src="https://github.com/user-attachments/assets/9b2fdcf6-18e5-4b88-8758-54b1ed90266f" />

# Question 9 
Identifying the source IP address used for lateral movement is essential for tracing the attacker's path and understanding the extent of the compromise. What is the IP address of the machine the attacker used to perform lateral movement to this Linux box?

- To find the source IP address, I used the command **grep -r "auth.log** to find authentication events.
<img width="1792" height="166" alt="image" src="https://github.com/user-attachments/assets/5624b1e8-d5ef-4a12-af32-bb537d165d1a" />

- I navigated to the **recup_dir.90** directory to find the auth.log events.
<img width="1642" height="381" alt="image" src="https://github.com/user-attachments/assets/aff8d30e-c27e-4327-9ca5-8787e1dfb887" />

- We can see the failed login attempts.

# Question 10
Identifying the first username targeted by the attacker in their brute-force attempts offers insight into their initial access strategy and target selection, as the attacker attempted to access two different accounts. What was the first username the attacker targeted in these brute-force attempts?


- Based on the logs in Question 9, we can see the account that the attacker tired to login as was root.

# Question 11
Determining the timestamp of the attacker’s final login is crucial for identifying when they last accessed the system to hide their activities and erase evidence. What is the timestamp of the last login session during which the attacker cleared traces on the compromised machine?

- To find the timestamp, I checked for when the attacker was successfully able to login to the accounts.
  - I looked for events with **"Accepted password"**.
    
<img width="1818" height="293" alt="image" src="https://github.com/user-attachments/assets/8bfb3598-ddff-40ec-9336-abd169a317af" />

- To find the year, I used **grep -r 192.168.19.147** to find the specific successful login.

# Question 12
During the attacker’s SSH session, they used a command that mistakenly saved their activities to the hard drive rather than keeping them in memory where they’d be more difficult to analyze. When the attacker ended their SSH session, which single bash command caused the shell to flush its in-memory command history to .bash_history on disk?

- To identify the command, I reviewed the **backup.elf** file.
  - I was able to find the exact command that the attacker used to end their SSH session. 
<img width="1234" height="590" alt="image" src="https://github.com/user-attachments/assets/136509fd-8ce4-4d8e-857c-310bea4426f7" />






























































