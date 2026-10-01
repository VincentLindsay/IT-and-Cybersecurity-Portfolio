# Overview
- This self-hosted project features a SOAR workflow utilizing Tines, and Lima Charlie as the EDR on a on-premises Windows Server version 2022.
   - The project involves the implementation of a SOAR playbook in Tines to send real-time Slack alerts, email notifications, and execute host isolation based on analyst feedback. 
   - Additionally, the simulation of a real-world password recovery attack on a monitored Windows VM to generate security telemetry, and validate custom-made a Lima Charlie detection.
# Project Topology
<img width="1197" height="802" alt="image" src="https://github.com/user-attachments/assets/ab6ffc5c-7f25-40a1-9198-0016f1017150" />

# Workflow Topology in Tines
<img width="1430" height="887" alt="image" src="https://github.com/user-attachments/assets/e6e0e11f-aa02-4db3-baae-61913bdebc3e" />



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
| 6 | Testing the Workflow | [View Section]

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

- To create the Automation Playbook, I integrated Slack Into Tines by creating an action block that sends a message into the SOAR+EDR channel
<img width="1302" height="600" alt="image" src="https://github.com/user-attachments/assets/745cc4e2-0855-4bc2-8c12-fe8e000c7ac2" />

- In order for Slack to have a message sent from Tines, I created a Slack application that will send a message into the SOAR+EDR channel
<img width="1917" height="897" alt="image" src="https://github.com/user-attachments/assets/3c5c7589-883c-44fd-90b8-4aeeef99b862" />

- I then created an action block for Tines to send an email
<img width="1291" height="422" alt="image" src="https://github.com/user-attachments/assets/267a272f-884c-4c1f-8b57-17b763db5493" />

- We can see that the email action worked as intended
<img width="980" height="287" alt="image" src="https://github.com/user-attachments/assets/20673a4e-a824-4262-b354-cb434eaff48a" />

- I then created a web page that will ask the Analyst to Isolate the endpoint, with an option of selecting Yes or No.
<img width="1632" height="932" alt="image" src="https://github.com/user-attachments/assets/a4e0fee6-6706-4f69-af26-53f887d4231b" />
<img width="652" height="397" alt="image" src="https://github.com/user-attachments/assets/86a3993f-c6a9-4547-bb7f-8ee20171c8e5" />

- I then configured Slack to send key fields like the Source IP address as a message.
<img width="391" height="797" alt="image" src="https://github.com/user-attachments/assets/a4baf163-6bff-4927-8515-7bcf568211fd" />

- We can see that the message contained key fields for identifying suspicious activity
<img width="1387" height="492" alt="image" src="https://github.com/user-attachments/assets/ef5da164-b1f6-4253-9ab0-c0bab4f98737" />

- Similarlly, I configured the email action block to also send the important fields.
   - We can now see that the email sent the desired fields. 
<img width="1537" height="492" alt="image" src="https://github.com/user-attachments/assets/576e3deb-6701-45c7-b882-a5adc6544e8d" />

- Furthermore, I also modified the user prompt page to include the fields.
<img width="695" height="471" alt="image" src="https://github.com/user-attachments/assets/ec095f34-f2ca-4596-95d7-8d115b202c5d" />

- I created a message block that will send the link to the page in the slack message
<img width="1402" height="610" alt="image" src="https://github.com/user-attachments/assets/8265c84c-d085-4521-8044-58fed519e46a" />
<img width="1737" height="751" alt="image" src="https://github.com/user-attachments/assets/9d9c3fef-03a4-45a5-b8a4-43d23c25316f" />

- I then added a condition that will send a slack message for the Analyst to investigate if the analyst chooses not to isolate the endpoint.
<img width="1312" height="575" alt="image" src="https://github.com/user-attachments/assets/bdb5f934-b5da-43f9-a0dc-0ca8aac35c4d" />
<img width="697" height="85" alt="image" src="https://github.com/user-attachments/assets/25a7eef1-6332-4b5d-bb2e-1ea1cd87405f" />

- After this, I configured the conditions if the analyst says yes to Isolate.
<img width="645" height="310" alt="image" src="https://github.com/user-attachments/assets/fbdc58a0-f22a-42f7-bd14-31479bd8b3b4" />

- If the Analyst selects yes from the web page, Lima Charlie will automatically begin to Isolate the endpoint.
   - And the Isolation of the Windows server was successful. 
<img width="1547" height="815" alt="image" src="https://github.com/user-attachments/assets/c34883f5-5d11-4fcd-b1e7-ce14c179d9ed" />
<img width="586" height="121" alt="image" src="https://github.com/user-attachments/assets/a6283f30-17c7-474c-b9e9-18f423271d73" />


- Additionally, the result of the Isolation will lead to a message being sent to the Analyst on Slack confirming the Isolation of the endpoint
<img width="367" height="412" alt="image" src="https://github.com/user-attachments/assets/6f19403e-15cd-4459-946e-ce7e3993271f" />
<img width="1387" height="115" alt="image" src="https://github.com/user-attachments/assets/5001e446-50d9-4737-8692-7246e678aeb0" />



# 6) Testing the Workflow
- The section involves the full test of the workflow assuming the Analyst Isolates the endpoint.
 - After the LaZagne program was executed, we can see the Incoming Email, and Slack messages
<img width="1402" height="610" alt="image" src="https://github.com/user-attachments/assets/4d2b2968-cef5-4b1d-b880-989e35d8ca0c" />
<img width="1502" height="386" alt="image" src="https://github.com/user-attachments/assets/0f443f44-abb8-4549-9251-a900cfbc3608" />
 
- The analyst accesses the prompt page and selects Yes.

<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/c9fdbfcb-d8c1-4165-af19-301101592cb0" />
- The Endpoint was automatically isolated










































































