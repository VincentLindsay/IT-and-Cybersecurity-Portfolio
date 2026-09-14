# Overview
- This project features the operation of a Microsoft-based cloud SOC lab using Sentinel, Defender for Endpoint, Defender for Office 365, and Entra ID.
  - I will configured and test email security policies (Safe Links, Anti-Phishing) and simulate phishing attacks to validate detections.
    - Additionally, I will write KQL queries to investigate failed logons, phishing attempts and endpoint alerts.
   
- The goal of this lab is to learn and complete as much as possible within the timespan of a Microsoft E5 trial.

# Table of Contents
- [ 1) Provisioning the Lab, and setting up Microsoft Sentinel](#1-Provisioning-the-Lab-and-setting-up-Microsoft-Sentinel)
- [ 2) Creating email security policies using Defender for Office 365]
- [ 3) Using Defender for Endpoint to create Endpoint security policies]
- [ 4) Creating Identity and Access management policies using Entra ID]



#  1) Provisioning the Lab, and setting up Microsoft Sentinel
- To begin with this project, I created an account for the Microsoft E5 Trial, and setup Azure.
- Since I named the company as "Phoenix Labs", with the Azure subscription being "Phoenix-Subscription" I created a Resource Group called **Phoenix-Vincent-RG**
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








