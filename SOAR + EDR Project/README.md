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
| 1 | Deploying Windows server & Lima Charlie | 
| 2 | Generating telemetry from the Windows server | 
| 3 | Creating a detection rule on Lima Charlie | 
| 4 | Developing the SOAR workflow using Slack and Tines | 
| 5 | Creating Automation Playbook within Tines | 

































































































