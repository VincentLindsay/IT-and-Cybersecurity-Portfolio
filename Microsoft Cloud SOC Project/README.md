# Overview
- This project is a a Microsoft Azure based SOC lab featuring Microsoft Sentinel, Defender XDR, Defender for Endpoint and Defender for Office 365 across threat detection, hunting, phishing investigation and incident response.
  - This project also involves the configuration and testing of email security policies (Safe Links, Anti-Phishing) and simulate phishing attacks to validate detection rules.

   
# Table of Contents
| Project Section No | Section Name | Section Link | Report link |  
| :---: | :---: | :---: | :---: |
| 1 | Provisioning the Lab, and setting up Microsoft Sentinel | [View section](#1-Provisioning-the-Lab-and-setting-up-Microsoft-Sentinel) | [View incident report](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/blob/main/Microsoft%20Cloud%20SOC%20Project/Project%20Reports/VLindsay-Brute%20Force%20Activity%20Report.pdf) |
| 2 | Creating email security policies using Defender for Office 365 | [View section](#2-Creating-email-security-policies-using-Defender-for-Office-365) | View incident report | 
| 3 | Using Defender for Endpoint to create Endpoint security policies | View section | View incident report |
| 4 | Creating Identity and Access management policies using Entra ID | View section | View incident report |
| A | KQL Queries | [View queries](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/tree/main/Microsoft%20Cloud%20SOC%20Project/KQL%20Queries) | [View my reports page](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/tree/main/Microsoft%20Cloud%20SOC%20Project/Project%20Reports) |



#  1) Provisioning the Lab, and setting up Microsoft Sentinel
- To begin with this project, I created an account for the Microsoft E5 Trial, and setup Azure.
- I created a resource group for the projects, with a naming convention of Phoenix-Vincent-()
<img width="1917" height="446" alt="image" src="https://github.com/user-attachments/assets/5c995000-b185-4214-b04c-cc3d3e9d09e6" />

- I then began to deploy a Windows 11 VM within the resource group.
<img width="1917" height="660" alt="image" src="https://github.com/user-attachments/assets/a021df00-4581-4d3b-b0e6-f61d19772a77" />

- After some time, the VM deployed to the resource group.
  - I then modified the networking settings to allow RDP traffic from my public IP address.
<img width="1502" height="300" alt="image" src="https://github.com/user-attachments/assets/b74021a2-9e81-463b-90a8-cc1f019b9d6a" />
 
- Now that the VM was setup, I can now begin with the deployment of Microsoft Sentinel.
  - To deploy Sentinel, I created a Log Analytics Workspace.
<img width="1097" height="511" alt="image" src="https://github.com/user-attachments/assets/6b1ce31d-9250-4ce8-be8c-86f3c839ae1b" />
<img width="1917" height="946" alt="image" src="https://github.com/user-attachments/assets/7dacd943-6e6a-4c0c-99ea-28b50f18e4ed" />

- Now that Sentinel was deployed, I began to utilize the Azure Sentinel Onboarding and training.
- Links: https://github.com/Azure/Azure-Sentinel/blob/master/Tools/Microsoft-Sentinel-Training-Lab/README.md
- https://github.com/Azure/Azure-Sentinel/blob/master/Tools/Microsoft-Sentinel-Training-Lab/Exercises/Onboarding.md

- After ingesting the training logs, I wrote my first KQL query: 
<img width="1166" height="825" alt="image" src="https://github.com/user-attachments/assets/4f1a63da-363d-4df7-afe9-2da4ba61fc22" />

- The first query views emails that were allowed to pass into a user's inbox, and contained the subject had the word "Urgent"
<img width="1167" height="822" alt="image" src="https://github.com/user-attachments/assets/221dd0bf-3369-4565-8b24-53caf290072e" />

- This query analyzes failed login events for an administrator account.
<img width="1177" height="841" alt="image" src="https://github.com/user-attachments/assets/4c88d146-8435-4ddf-a9f0-4c101b0096f0" />

- This last query views the number of EventIDs in a Windows environment.

- I created three different visualizations based on the previous queries.
<img width="1410" height="842" alt="image" src="https://github.com/user-attachments/assets/e4aa0386-b966-4ff5-8084-28e400d6f13f" />

- For instance, this Pie chart represents the top 5 failed logins by user.

- With the help of ChatGPT, I created a bar chart that sorts the logins by top 5 users within an hour of the training data.
<img width="1536" height="937" alt="image" src="https://github.com/user-attachments/assets/53564f55-c40c-4dac-b09c-25fc2a2f33b5" />

- I also created a timechart as well that follows a similar format as the Pie Chart
<img width="1486" height="750" alt="image" src="https://github.com/user-attachments/assets/af60773e-c774-452c-8ad4-ee18e044d4ee" />

- Furthermore, I did create an alert based on the training data that checks for failed login attempts with a threshold of 1000 events.
<img width="1540" height="935" alt="image" src="https://github.com/user-attachments/assets/12e1a64b-8ed4-4f22-a8e1-d902463229df" />

- After some time, we can see that the alert triggered in Microsoft Sentinel's Incidents page.
<img width="1562" height="815" alt="image" src="https://github.com/user-attachments/assets/61bdc164-c808-4d16-a88d-82647b2b839f" />

# 2) Creating email security policies using Defender for Office 365
- To begin, I created two user accounts that will be used to test email security policies.
<img width="1432" height="230" alt="image" src="https://github.com/user-attachments/assets/d57b682b-a25a-4496-bbd7-c89f24988f26" />

- Once the users were created, I also created the outlook mailboxes for the accounts.
<img width="1905" height="270" alt="image" src="https://github.com/user-attachments/assets/269bb116-17c4-43a9-b9df-eb9c3cda1257" />
<img width="1917" height="645" alt="image" src="https://github.com/user-attachments/assets/3c790ccc-6a0c-49d1-a9f8-f6ab336759ab" />

- In Microsoft Defender XDR, we can see the emails for the newly created accounts.
<img width="1492" height="497" alt="image" src="https://github.com/user-attachments/assets/8a8d2fc4-0dee-4e1b-a231-3cf3a4ec88f7" />

- With the test accounts, I created a safelinks policy using Microsoft Defender XDR
<img width="1916" height="952" alt="image" src="https://github.com/user-attachments/assets/d0417f63-7fdf-4aa3-9c9d-8d54db70f0e9" />

- Once the policy was created, I sent an email to one of the test accounts to test the policy.
<img width="1917" height="1002" alt="image" src="https://github.com/user-attachments/assets/ce19bfe4-0ec8-45de-b6a0-33bc718c3580" />

- We can see that the safelinks policy worked as intended.
- Once I created the safelinks policy, I proceeded to create an anti-phishing policy that is domain wide.

These user accounts have impersonation protection enabled.
  - Michael Scott
  - Vincent Lindsay (my Global Admin. Account)
<img width="1917" height="991" alt="image" src="https://github.com/user-attachments/assets/0426346a-94cf-4b1e-b0dd-8777b69c9e18" />

- I also enabled behavior based impersonation protection as well.
<img width="1397" height="897" alt="image" src="https://github.com/user-attachments/assets/0746704d-e175-4d28-8817-11c0741b71e5" />
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/dca4750f-ec6c-43dd-a15a-4d18cb869d9f" />

- With that in mind, the anti-phishing policy was created.
<img width="1535" height="481" alt="image" src="https://github.com/user-attachments/assets/14937907-3ca9-4573-915a-33a0c691571d" />

- To test the phishing policies, I sent an email to one of the user accounts with a fake phishing email that contains a link to a webpage.
<img width="745" height="372" alt="image" src="https://github.com/user-attachments/assets/68d78e2c-7546-466b-b65c-46e10897bcb6" />

- We can also see that the anti-phishing policy worked, giving the user safety tips like the receiving of an email from the sender.
<img width="1919" height="988" alt="image" src="https://github.com/user-attachments/assets/f093d858-4d14-46df-92ad-05d03ac57541" />

- To mimic phishing, I utilized the phishing campaign service from Microsoft, and the campaign revolves around credential harvesting
<img width="1592" height="832" alt="image" src="https://github.com/user-attachments/assets/2a703a40-5072-47cd-83d1-e1d9b177407c" />

- In this case, the user views the email, clicks the link, and enters their respective credentials to login.
<img width="1917" height="952" alt="image" src="https://github.com/user-attachments/assets/215ac6ea-2070-4c1f-998c-910808df8d09" />

- As a result, the user was assigned training.
<img width="1917" height="1000" alt="image" src="https://github.com/user-attachments/assets/403fe936-26a6-4c2c-bd45-d9e82049f28f" />










































