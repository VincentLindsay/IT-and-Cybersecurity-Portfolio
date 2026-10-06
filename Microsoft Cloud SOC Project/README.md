- This project is a a Microsoft Azure based SOC lab featuring Microsoft Sentinel, Defender XDR, Defender for Endpoint and Defender for Office 365 across threat detection, hunting, phishing investigation and incident response.
  - This project also involves the configuration and testing of email security policies (Safe Links, Anti-Phishing) and simulate phishing attacks to validate detection rules.

   
# Table of Contents
| Project Section No | Section Name | Section Link | Report link |  
| :---: | :---: | :---: | :---: |
| 1 | Provisioning the Lab, and setting up Microsoft Sentinel | [View section](#1-Provisioning-the-Lab-and-setting-up-Microsoft-Sentinel) | [View incident report](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/blob/main/Microsoft%20Cloud%20SOC%20Project/Project%20Reports/VLindsay-Brute%20Force%20Activity%20Report.pdf) |
| 2 | Creating email security policies using Defender for Office 365 | [View section](#2-Creating-email-security-policies-using-Defender-for-Office-365) | [View incident report](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/blob/main/Microsoft%20Cloud%20SOC%20Project/Project%20Reports/VL_Phishing_Investigation.pdf) | 
| 3 | Using Defender for Endpoint to create Endpoint security policies | [View section](#3-Using-Defender-for-Endpoint-to-create-Endpoint-security-policies) | [View incident report](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/blob/main/Microsoft%20Cloud%20SOC%20Project/Project%20Reports/VL_Alert_Investigation.pdf) |
| 4 | Creating Identity and Access management policies using Entra ID | [View section](#4-Creating-Identity-and-Access-management-policies-using-Entra-ID) | View end to end Investigation report |
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

- Moving forward, I created a test proton mail account to simulate another phishing attack.
  - In this case, the user Dwight received an email claiming to be Michael discussing a change in Dwight's compensation.
  - The email also includes a simulated document containing a link.
<img width="1605" height="737" alt="image" src="https://github.com/user-attachments/assets/10f22527-1d74-446e-b01c-2937c4443b4e" />
<img width="1534" height="202" alt="image" src="https://github.com/user-attachments/assets/c46e7262-0150-45c3-817a-1ac9924b52f3" />

- View the reports page to view my report on a simulated phishing email. 

# 3) Using Defender for Endpoint to create Endpoint security policies
- In this section, I will utilize Microsoft Defender for Endpoint to monitor endpoint telemetry generated by the Windows 11 VM created in section 1
  - Prior to onboarding the VM into the EDR, I enabled the following settings:
    -  Enable EDR in block mode
    -  Web content filtering
    -  Custom network indicators

- These behavior based settings allow the EDR to actively response to suspicious activity
<img width="1072" height="126" alt="image" src="https://github.com/user-attachments/assets/93f8c245-9d73-4bd0-9be6-efb2d742e685" />
<img width="1060" height="147" alt="image" src="https://github.com/user-attachments/assets/fa406e46-bcda-4232-9532-e315af0b0957" />
<img width="1047" height="146" alt="image" src="https://github.com/user-attachments/assets/5bd3bff0-bce6-4149-b8ec-eb358bb8be5a" />

- I onboarded the Azure VM locally using the PowerShell Script, and downloaded the onboarding package.

<img width="1527" height="666" alt="image" src="https://github.com/user-attachments/assets/f24dfede-0fe3-44ff-8bad-70e6755a931b" />

- After executing the onboarding program, and the connectiion test PowerShell script, the Windows 11 VM was onboarded onto Microsoft Defender for Endpoint.
  - In addition to onboarding the VM into Microsoft Defender for Endpoint, I also created a device-specific Microsoft Intune policy utilizing the attack surface reduction (ASR) rules.
  - I enabled features such as the blocking of "Block credential stealing from the Windows local security authority subsystem". 
<img width="1632" height="942" alt="image" src="https://github.com/user-attachments/assets/5fa9ecec-4496-4ae4-9449-665f2057795d" />
<img width="1640" height="950" alt="image" src="https://github.com/user-attachments/assets/b854c839-c0a0-48c2-a9f4-89095fbac791" />


- I also assigned the VM the newly created Intune ASR policy, as well as Entra ID
<img width="812" height="772" alt="image" src="https://github.com/user-attachments/assets/b37400a2-2ec6-48d1-9ee3-56e8803d4ca6" />

- To further verify that the VM was correctly implemented into MDE, I installed atomic red team into the VM
<img width="1072" height="300" alt="image" src="https://github.com/user-attachments/assets/ca827892-9ad9-41ff-9616-a4a8a0a47324" />
<img width="1086" height="80" alt="image" src="https://github.com/user-attachments/assets/71331707-b7eb-4774-a824-2e2a3d721f79" />

- Once Installed, I ran a test of MITRE Technique T1547.001, which refers to "Boot or Logon Autostart Execution: Registry Run Keys / Startup Folder"
  - In this case, I am emumlating the addition of persistence mechanisms via Windows Registry
 <img width="1082" height="602" alt="image" src="https://github.com/user-attachments/assets/d879580c-1ccf-4954-8817-8e76d75cad60" />

- Once the test completed, the activity triggered numerous alerts on MDE
<img width="1480" height="486" alt="image" src="https://github.com/user-attachments/assets/830b1b76-4620-458e-b965-ded4301c2554" />

- I ran another test that utilizes MITRE Technique T1685.005, which refers to the Defense Impairment Technique of Disable or Modify Tools: Clear Windows Event Logs
<img width="1391" height="667" alt="image" src="https://github.com/user-attachments/assets/9bfc97ba-596c-4a7e-818d-eab11492a656" />

- The test worked, however, MDE treated the activity as Ransomware, and automatically isolated the VM, and contained the account associated with the Ransomware-like behavior
<img width="1531" height="927" alt="image" src="https://github.com/user-attachments/assets/f7a565bb-0044-4bbb-8c13-35d8bdeb745c" />
<img width="1536" height="932" alt="image" src="https://github.com/user-attachments/assets/03d7690b-04c4-4a6e-b24d-ff1d82679742" />

- As result, I began to remidate the activity via undoing the automatic endpoint isolation, and containment of the user account - Michael

# 4) Creating Identity and Access management policies using Entra ID
- This section features the creation of several IAM policies such as a conditional access policy

- This conditional access policy will only allow sign ins from the domain, and will block any sign in from outside IP addreeses

- In this case, I replicated normal sign in behavior as well as risky sign-ins from Singapore using a VPS geolocated in Singpore

<img width="1022" height="480" alt="image" src="https://github.com/user-attachments/assets/0c545f82-c309-40c3-9c16-96a61fcee455" />

- Although the location is displayed as Japan (JP), the IPv6 address matches the IP address in the VPS.
<img width="1917" height="476" alt="image" src="https://github.com/user-attachments/assets/14becf10-3589-4e7c-945b-0d1aa9bc5401" />

- As a result, the user account had a risky sign in.
<img width="1917" height="477" alt="image" src="https://github.com/user-attachments/assets/c8d487f9-2b04-4622-9c28-4be2aaafa424" />

- I created a country blocklist based on the IP address.
<img width="1917" height="517" alt="image" src="https://github.com/user-attachments/assets/cbb809d9-6324-4341-82d0-fcd36093a678" />

- I then created the Conditional Access Policy that blocks access from the country blocklist
<img width="1917" height="712" alt="image" src="https://github.com/user-attachments/assets/8177b303-befc-415c-b3c8-b9c737ae17ce" />

- After testing the policy, we can see that the policy was successfully configured
<img width="1517" height="837" alt="image" src="https://github.com/user-attachments/assets/1b36c9a0-64ec-44ed-b4e3-55253d419794" />
<img width="1067" height="890" alt="image" src="https://github.com/user-attachments/assets/fc2a7205-1430-4388-89b9-b0c2f96f9a7f" />

- To unify all log sources within Microsoft Sentinel, I added the Entra ID data connector to Sentinel.
  - I installed the Entra ID workspace into Sentinel, and configured the data connector to Ingest the Sign-in and Audit logs. 
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/c2ef9d93-54a0-4f3c-bc7c-c5c0bc7f4aad" />
<img width="1917" height="947" alt="image" src="https://github.com/user-attachments/assets/5e2953b1-ea63-4c23-8c53-17e068f2b4ac" />

- I then tested the log ingested by signing into one of the test accounts, and queried the login event.
<img width="1217" height="822" alt="image" src="https://github.com/user-attachments/assets/e8357b07-38a2-4b93-a657-cb00295a8a7a" />

































