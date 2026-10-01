# Overview
- This self-hosted project features a SOAR workflow utilizing Tines, and Lima Charlie as the EDR on a on-premises Windows Server version 2022.
   - The project involves the implementation of a SOAR playbook in Tines to send real-time Slack alerts, email notifications, and execute host isolation based on analyst feedback. 
   - Additionally, the simulation of a real-world password recovery attack on a monitored Windows VM to generate security telemetry, and validate custom-made a Lima Charlie detection.
# Project Topology
<img width="1197" height="802" alt="image" src="https://github.com/user-attachments/assets/ab6ffc5c-7f25-40a1-9198-0016f1017150" />


# Playbook Workflow
- The Automation Playbook's logic is as follows:
  * A) An alert is Triggered on Lima Charlie.
  * B) The alert is Forwarded to Tines, where the alert will be sent to Slack, and an email regarding the alert.
  * C) After the Slack message, and email, a user prompt will appear in the Slack message, prompting the user to Isolate an Endpoint.
  * D) If the User selects Yes, Lima Charlie will perform endpoint isolation.
  
# Table of contents 
| Project Section No | Section Name | Section Link | 
| :---: | :---: | :---: | 
| 1 | Deploying Windows server 2019 and Lima Charlie | [View Section](#1-Deploying-Windows-server-2019-and-Lima-Charlie) | 
| 2 | Generating telemetry from the Windows server using LaZagne | [View Section](#2-Generating-telemetry-from-the-Windows-server-using-LaZagne) |
| 3 | Creating a LaZagne detection rule in Lima Charlie | [View Section](#3-Creating-a-LaZagne-detection-rule-in-Lima-Charlie) | 
| 4 | Developing the SOAR workflow using Slack and Tines | [View Section](#4-Developing-the-SOAR-workflow-using-Slack-and-Tines) |
| 5 | Creating the Automation Playbook within Tines and Slack | [View Section](#5-Creating-the-Automation-Playbook-within-Tines-and-Slack) |


# 1) Deploying Windows server 2019 and Lima Charlie  
- I was able to retrieve an ISO file from Microsoft's evaluation center page.
   - Here is a link: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019

<img width="1026" height="777" alt="image" src="https://github.com/user-attachments/assets/47e623a6-d26f-4680-bdad-09d24ffe8c95" />

- I Installed the Windows server with the following specs:
   - 2 CPUS
   - 6 GB of RAM
   - 75 GB of storage

- Once the server Installed, I began the process of installing Lima Charlie onto the Windows server.

- In Lima Charlie, I setup an account, and created an Organization, as well as an installation key for the project.
<img width="1547" height="366" alt="image" src="https://github.com/user-attachments/assets/ff043be1-4920-453a-9069-13ba6d3154ad" />

- Once I downloaded the exectuiable using the installation key I created, Lima Charlie was installed.
<img width="1522" height="451" alt="image" src="https://github.com/user-attachments/assets/90fb6dc2-24b0-41f4-b028-9a157f0a6a89" />

- We can see that the server is successfully displayed on Lima Charlie

# 2) Generating telemetry from the Windows server using LaZagne
- Using the LaZagne tool, I simulated a password recovery attack that focuses on credential harvesting.
- link to the tool: https://github.com/alessandroz/lazagne
   - Once I downloaded the python executable, I ran the program to verify that it works, and that Lima Charlie can detect the exection of the process from PowerShell
<img width="851" height="237" alt="image" src="https://github.com/user-attachments/assets/53ce0c93-2b37-4b92-88e8-aecd972e939a" />

- We can see that the process execution was detected on Lima Charlie
<img width="1452" height="457" alt="image" src="https://github.com/user-attachments/assets/de521a01-f655-422c-a83d-c5777b4e58cb" />

- By looking at the details of the event, we can see evidence such as the File path associated with the process.
   - In section 3, I created a detection and reponse (D&R) rule to identify LaZagne based credential harvesting attempts. 
<img width="727" height="641" alt="image" src="https://github.com/user-attachments/assets/2d7dbd64-525e-4bee-95cb-ec2842077ee2" />

# 3) Creating a LaZagne detection rule in Lima Charlie
- This section follows section 2, where I simulated credential harvesting using LaZagne.
   - This section focuses on the creation of a Detection and Response (D&R) rule that focuses on identifying the usage of LaZagne on the Windows server.
 
- To begin with the D&R rule, I first began creating the Detection rule, and the rule detects the following:
   - The rule detects newly created and existing processes on a Windows machine
   - The rule also dectects LaZagne usage if the file path ends with LaZagne.exe
   - The rule will also identify any command line usage associated with Lazagne
<img width="1765" height="447" alt="image" src="https://github.com/user-attachments/assets/a6a3cb57-9a32-42e3-94be-91b36ed3ca19" />

- On the other hand, the Response rule will tell Lima Charlie to generate a Detection alert. 
<img width="992" height="351" alt="image" src="https://github.com/user-attachments/assets/3dabcb59-443e-4738-ae06-4b9dfc13cab3" />

- Prior to conducting a live test of the alert, I used an ealrier event to test the alert I created.
<img width="846" height="740" alt="image" src="https://github.com/user-attachments/assets/46ff3682-5351-4d4b-84d3-f9b0755594c0" />


- Once the detection rule was created, I executed LaZagne again to verify that the D&R rule worked as intended
<img width="1531" height="316" alt="image" src="https://github.com/user-attachments/assets/ea98b15b-8afb-47ce-89e8-4ca754a910cd" />

- We can see that the rule creation was successful.

# 4) Developing the SOAR workflow using Slack and Tines
- In my [Wazuh Project](https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/tree/main/Wazuh%20Project), I used Slack and Tines in a similar manner.
   - Since I have a Slack workspace already created, I made a chat channel dedicated to this project: SOAR + EDR
<img width="1911" height="757" alt="image" src="https://github.com/user-attachments/assets/e3f5667d-46bd-42d3-8d58-e528f89cc109" />

 - Once I created the Slack Channel, I began to create the SOAR playbook within Tines.
    - To fully configure the Webhook, I configured the output stream in Lima Charlie, that outputs the detection alerts from Lima Charlie into Tines
<img width="1872" height="582" alt="image" src="https://github.com/user-attachments/assets/b4fe9d34-ca6a-4a7d-9969-3a6b9bfbb662" />
- The output was created, but to test the configurations, I executed the LaZagne program again to test the output.
<img width="1166" height="905" alt="image" src="https://github.com/user-attachments/assets/26338cd1-d253-4dcd-ad84-38f7a1795dd3" />

- The Alert was successfully transferred into Tines.
- Now that the webhook was successfully configured, I began to configure the Automation Playbook in Tines and Slack.


# 5) Creating the Automation Playbook within Tines and Slack





















































































