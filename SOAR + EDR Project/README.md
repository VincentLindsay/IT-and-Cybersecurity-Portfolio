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
| 1 | Deploying Windows server 2019 & Lima Charlie | [View Section](#1-Deploying-Windows-server-2019-&-Lima-Charlie) | 
| 2 | Generating telemetry from the Windows server | 
| 3 | Creating a detection rule on Lima Charlie | 
| 4 | Developing the SOAR workflow using Slack and Tines | 
| 5 | Creating Automation Playbook within Tines | 


# 1) Deploying Windows server 2019 & Lima Charlie  
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

# 2) Generating telemetry from the Windows server


























































































