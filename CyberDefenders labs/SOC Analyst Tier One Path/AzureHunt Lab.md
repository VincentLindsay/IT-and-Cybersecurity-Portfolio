# Overview
- Lab link: https://cyberdefenders.org/blueteam-ctf-challenges/azurehunt/
<img width="1918" height="428" alt="image" src="https://github.com/user-attachments/assets/8a6da0b8-8b90-4ea9-81e5-619dc63c0667" />

# Scenario
A finance company's Azure environment has flagged multiple failed login attempts from an unfamiliar geographic location, followed by a successful authentication. Shortly after, logs indicate access to sensitive Blob Storage files and a virtual machine start action. Investigate authentication logs, storage access patterns, and VM activity to determine the scope of the compromise.

# Question 1
As a US-based company, the security team has observed significant suspicious activity from an unusual country. What is the name of the country from which the attack originated?

- Since we know that the Company is based in the US, I checked viewed the **source.geo.country_name.keyword** filter, and found activity outside the US.
<img width="1908" height="1001" alt="image" src="https://github.com/user-attachments/assets/c5b7493a-82e4-4377-896a-700652e0aced" />

# Question 2
To establish an accurate incident timeline, what is the timestamp of the initial activity originating from the country?

- To find the initial activity, I filtered by Germany, and the timeline in descending order.
<img width="1918" height="692" alt="image" src="https://github.com/user-attachments/assets/0dd0c4c9-1852-49fd-93e1-dd379688e017" />


# Question 3 
To assess the scope of compromise, we must determine the attacker's entry point. What is the display name of the compromised user account?
- By searching for sign-in activity from Germany, I found that an account by the name of **alice** was signed into from Germany.
<img width="1925" height="997" alt="image" src="https://github.com/user-attachments/assets/126c397a-2b89-41a8-b2ed-26cd79be7170" />


# Question 4
To gain insights into the attacker's tactics and enumeration strategy, what is the name of the script file the attacker accessed within blob storage?

- To find the attacker's tactics, I checked the **azure.eventhub.category** field, and viewed the StorageRead value.
<img width="876" height="752" alt="image" src="https://github.com/user-attachments/assets/9a2ca493-52af-488d-a5f4-fb71d50a54c0" />

- Since we know that the attacker also enumerated blob storage, I also viewed the contents of the **azure.eventhub.operationName.keyword: GetBlob** field
<img width="1917" height="1007" alt="image" src="https://github.com/user-attachments/assets/13bf952a-449c-4955-9d99-615c60e1a02e" />

- We can see the retrieved script file.


# Question 5
For a detailed analysis of the attacker's actions, what is the name of the storage account housing the script file?

- We can see the name of the storage account that holds the script
<img width="965" height="903" alt="image" src="https://github.com/user-attachments/assets/c0c4992f-7b8d-4905-92e4-fcd7aa707b0f" />

# Question 6
Tracing the attacker's movements across our infrastructure, what is the User Principal Name (UPN) of the second user account the attacker compromised?

- To confirm the second compromised account, I filtered UPN's by Germany, and found an account called IT Admin that had the most events.
<img width="1918" height="1010" alt="image" src="https://github.com/user-attachments/assets/963a0cd9-b293-46f9-a854-b64fdfba4166" />


# Question 7
Analyzing the attacker's impact on our environment, what is the name of the Virtual Machine (VM) the attacker started?
- By filtering for resource names, I was able to find the name of the VM the attacker started.
<img width="1913" height="995" alt="image" src="https://github.com/user-attachments/assets/11f19537-d2f5-4945-9e8a-dd3e23756988" />


# Question 8
To assess the potential data exposure, what is the name of the database exported?
- By filtering events that pertain to the compromised admin account, I was able to find the exported database.
<img width="1918" height="992" alt="image" src="https://github.com/user-attachments/assets/dcfc2a44-fdeb-4296-b3d4-0a9c98b643ee" />


# Question 9 
In your pursuit of uncovering persistence techniques, what is the display name associated with the user account you have discovered?

- To find persistence, I checked the audit logs, and found events with the **add user** value.
- We can see the created user account.
<img width="1918" height="1006" alt="image" src="https://github.com/user-attachments/assets/464ea478-c7ab-416f-9c1e-de719fee3190" />

# Question 10
The attacker utilized a compromised account to assign a new role. What role was granted?
- When filtering by **azure.activitylogs.identity.authorization.evidence.role** to look for any roles added to the new account, I found the role that the account was added as an owner.
<img width="1918" height="1002" alt="image" src="https://github.com/user-attachments/assets/1f487c27-3c5f-4def-8de2-b0c78e64b6ad" />



# Question 11
For a comprehensive timeline and understanding of the breach progression, What is the timestamp of the first successful login recorded for this user account?

- By using a keyword search of the account, name, I was able to find the initial login for the account.
<img width="1918" height="970" alt="image" src="https://github.com/user-attachments/assets/61156ccd-8a23-48cf-afb5-d43ef8232000" />
































