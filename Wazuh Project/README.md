# Overview
- This projects entails the setup and configuration of Wazuh, following a similar format to the Splunk lab, where I will showcase complete my learning of Wazuh.

- This lab will also showcasing using an AI Agent as a SOC analyst to identify malicious activity.
  - Direct link to the Splunk lab: https://github.com/VincentLindsay/IT-and-Cybersecurity-Portfolio/tree/main/Splunk%20lab
  - I will also write a report of an investigation of Malicious activity.
 
# Machines & tools used in this lab
- VMware Workstation Pro
  - VMware is the hypervisor.

- Ubuntu Server 24.04
  - Used for Wazuh.

- Windows 10 Pro
  - This machine will serve as the Endpoint, and the victim machine. 

# Table of Contents
- [ 1) Deploying the Wazuh server](#1-Deploying-the-Wazuh-Server)
- [ 2) Deploying the Windows 10 endpoint](#2-Deploying-the-Windows-10-endpoint)
- [ 3) Installing the Ubuntu endpoint](#3-Installing-the-Ubuntu-endpoint)
- [ 4) Installing Wazuh](#4-Installing-Wazuh)
- [ 5) Installing Wazuh Agents](#5-Installing-Wazuh-Agents)
- [ 6) Installing Sysmon on the endpoints](#6-Installing-Sysmon-on-the-endpoints)
- [ 7) Generating & reading telemetry](#7-Generating-&-reading-telemetry)
- [ 8) Creating a dashboard](#8-Creating-a-dashboard)
- [ 9) Implementing File Integrity Monitoring]
- [ 10) Setting up SOAR]
- [ 11) Creating a C2 Server]
- [ 12) Active Response to a detection]
- [ 13) Investigating the instruction]


# 1) Deploying the Wazuh Server
- To deploy the Wazuh server, I first started with the deployment of the Ubuntu Server via retrieving the ISO from Ubuntu's download page
  - Direct link: https://ubuntu.com/download/server
 
- Once the ISO was downloaded, I began the installation of the vm.
- I selected the ISO file.
<img width="502" height="537" alt="image" src="https://github.com/user-attachments/assets/216c8f95-a1f7-442a-bdb4-3af564717e52" />

- I began to configure the VM.
<img width="1918" height="1038" alt="image" src="https://github.com/user-attachments/assets/bad130e8-35e0-44e9-9806-4ea1e2ed9ef6" />

- In the vm's configuration settings, I did choose to install the OpenSSH server so that configuration is much easier.
<img width="1326" height="877" alt="image" src="https://github.com/user-attachments/assets/2c34f280-e662-453d-8237-d39f2de7a208" />

- Once logged into the server, I began to update the packages.
<img width="957" height="718" alt="image" src="https://github.com/user-attachments/assets/79a6249b-897c-4eae-8d33-eb9a534a7852" />

- Once the updates were complete, I also created a snapshot prior to installing Wazuh.
<img width="957" height="837" alt="image" src="https://github.com/user-attachments/assets/08ccfb6c-9187-4825-b910-50fbef229856" />


# 2) Deploying the Windows 10 endpoint
- To deploy the Windows endpoint, I retrieved an ISO from Microsoft's download page.
  - Direct link: https://www.microsoft.com/en-us/software-download/windows10%5B1%5D

- To get the ISO, I used the media creation tool.
<img width="802" height="721" alt="image" src="https://github.com/user-attachments/assets/edba79a7-69e3-40f9-a20b-7be3576e76d8" />

- Select the option to create an installation media.
- Create the ISO file.
<img width="790" height="702" alt="image" src="https://github.com/user-attachments/assets/74a3d023-6e03-4d62-b583-715fc4e86abf" />

- After some time the ISO file will be created.
<img width="1916" height="1040" alt="image" src="https://github.com/user-attachments/assets/7acd880e-b65b-41ed-9a4c-c28b8dccad5b" />

- These were the settings I had for the vm.
  - I chose a custom installation of Windows 10 Professional.

 - After sometime, I created a user account for the Endpoint, and created a snapshot
<img width="1022" height="772" alt="image" src="https://github.com/user-attachments/assets/2e525d99-37ea-466a-b7c6-1bbe9faa7679" />

- I also enabled remote desktop to simplify configurations.
<img width="801" height="646" alt="image" src="https://github.com/user-attachments/assets/8ef5977c-6a8a-4574-a49b-a07d4542a8bd" />



# 3) Installing the Ubuntu endpoint
- The deployment of the Ubuntu endpoint followed the same process as the Wazuh server.
<img width="1918" height="1041" alt="image" src="https://github.com/user-attachments/assets/c020a7ee-0927-4d61-987e-7c77db1b9c8a" />

- I also installed the OpenSSH server.
<img width="1351" height="892" alt="image" src="https://github.com/user-attachments/assets/0bd2840e-8b30-40db-ac00-9729b23b9c0f" />

- I also updated the packages for the endpoint.
<img width="1132" height="837" alt="image" src="https://github.com/user-attachments/assets/8fb69e9f-b2ed-4b11-a589-255c246d9b8e" />

- I also created a screenshot.

# 4) Installing Wazuh
- To install Wazuh, I navigated to the quickstart installation
  - Direct link: https://documentation.wazuh.com/current/quickstart.html

<img width="1648" height="646" alt="image" src="https://github.com/user-attachments/assets/debaa561-4ad1-442f-98a6-4bab25c380b9" />

- After sometime, Wazuh finished installing
<img width="1660" height="232" alt="image" src="https://github.com/user-attachments/assets/0efab1db-c65d-4b7a-97cf-a1cb28e7f87b" />


- I was successfully able to log into the Wazuh web interface
<img width="1918" height="1086" alt="image" src="https://github.com/user-attachments/assets/3851e192-ba13-47c8-bfbd-72705de84f76" />

- Next, I began to configure archives for Wazuh.
<img width="1916" height="116" alt="image" src="https://github.com/user-attachments/assets/9ffba58f-947e-4d1b-be2b-96e8326add2a" />

- I am specifically changing the **ossec.conf** file.
<img width="1406" height="98" alt="image" src="https://github.com/user-attachments/assets/802c4462-60d9-446f-b9ca-69018ce228d7" />

- I changed the **logall**, and the **logall_json** configuration to yes
<img width="1137" height="648" alt="image" src="https://github.com/user-attachments/assets/8ab0c538-b65b-4781-a9d8-82e41ca33a3f" />

- After making the configuration changes, I restarted the Wazuh manager service.
- I also began to change the file beat configuration to enable archives logging.
<img width="1218" height="106" alt="image" src="https://github.com/user-attachments/assets/31a56328-b463-41d9-ae77-de1e1d0b0a94" />

- I enabled the archives option on the file beat configuration settings.
  - After the configuration settings were applied, I restarted the Wazuh manager service.
<img width="1627" height="1043" alt="image" src="https://github.com/user-attachments/assets/e2546c1b-a75d-493b-bbdc-0c26542e0cc8" />

- I also created an index called **Wazuh-archives** 
<img width="1552" height="478" alt="image" src="https://github.com/user-attachments/assets/ba365f05-cf22-4d28-88a9-f1362024a4ec" />

- The index also uses timestamp as the time field.
<img width="1515" height="667" alt="image" src="https://github.com/user-attachments/assets/0262207a-1df4-4923-bcd6-eb3326dffa68" />

- We can now see the successful creation of the new index.
  - I also created a snapshot of the progress so far. 

# 5) Installing Wazuh Agents
- To install the Agents, I started with the installation of Wazuh Agent on the **Windows** endpoint.
<img width="1917" height="937" alt="image" src="https://github.com/user-attachments/assets/1daf89c2-6872-4e42-ae89-ca134e2dd47b" />

- I gave the configuration of the server's IP address, as well as the Agent name for the Windows endpoint.
  - Furthermore, I started the installation of the agent.
<img width="1911" height="571" alt="image" src="https://github.com/user-attachments/assets/3be807eb-64ad-4237-820e-bd7b0670c4ac" />


- We can now see that the Wazuh agent was installed successfully on the Windows endpoint.
  - I created a snapshot of the agent's installation. 

- Next, I began to install the agent on the Ubuntu endpoint.
  - The process is similar to the Windows endpoint.
<img width="1912" height="1080" alt="image" src="https://github.com/user-attachments/assets/4dbfa02f-05e7-4ddd-800d-cbaafd214ef3" />

- The packages for the agent were installed.
<img width="1907" height="477" alt="image" src="https://github.com/user-attachments/assets/72256f71-8832-431f-a199-0231a408d59a" />

- Next, I entered the commands to start the service for Wazuh.
<img width="1611" height="97" alt="image" src="https://github.com/user-attachments/assets/41a51789-ee6d-4008-aab7-47d63fd67b95" />

- We can now see the successful deployment of two agents.
<img width="1918" height="670" alt="image" src="https://github.com/user-attachments/assets/806a0264-28e3-46ae-b9e9-c5e701faff10" />

- Now I will install, and configure Sysmon on the Windows and Ubuntu endpoints.

# 6) Installing Sysmon on the endpoints
- I will install Sysmon on the Windows, and Ubuntu endpoint's
  - I first began to install Sysmon on the Windows endpoint.
<img width="1912" height="553" alt="image" src="https://github.com/user-attachments/assets/a3cc803e-3815-4de9-b33b-0cc25c9fa24d" />

- For the configuration file, I used the Olaf Hartong Configuration file.
  - Direct link: https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml
  - I saved the XML file to the Windows endpoint.
<img width="1918" height="587" alt="image" src="https://github.com/user-attachments/assets/867c64ca-f9af-4e84-a80b-ca57df83c990" />

- After downloading both Sysmon, and the configuration file, I began to install Sysmon.
<img width="1918" height="420" alt="image" src="https://github.com/user-attachments/assets/3a194c86-5d77-45c8-9c9a-9580d7bfa53c" />

- Now Sysmon is installed on the Windows Endpoint.
  - I also changed the **ossec.conf** configurations to allow the endpoint to forward Sysmon logs.
<img width="1432" height="688" alt="image" src="https://github.com/user-attachments/assets/cae11f06-a38b-4d9b-8822-818c3508e8cd" />

- We can see that the configurations were successful.
<img width="1918" height="1042" alt="image" src="https://github.com/user-attachments/assets/251ef346-0ea1-4ed3-963c-6a982a0a31df" />

- Next, I installed Sysmon on the Ubuntu endpoint.
  - Direct link: https://github.com/microsoft/SysmonForLinux/blob/main/INSTALL.md

- I entered the commands for an Ubuntu installation.
<img width="1912" height="248" alt="image" src="https://github.com/user-attachments/assets/3aa3ef62-5ccb-4a36-abe0-27ee4b273f15" />


- I also added a configuration file to the Sysmon settings.
  - Direct link: https://raw.githubusercontent.com/microsoft/MSTIC-Sysmon/refs/heads/main/linux/configs/collect-all.xml

- Now Sysmon is installed.
<img width="1917" height="350" alt="image" src="https://github.com/user-attachments/assets/26deaf4f-540a-4093-8110-84ba93787fdc" />

- We can now see the Ubuntu endpoint Sysmon logs.

# 7) Generating & reading telemetry
- To verify that all logs are properly ingested into Wazuh, I generated some telemetry using the Windows endpoint.
  - For instance, I intentionally incorrectly entered the password of the user account 

<img width="1522" height="922" alt="image" src="https://github.com/user-attachments/assets/2f092092-6bb6-400e-b5d8-221915a07fd8" />
- In this log, we can see that an account was successfully logged into by an interactive login.

<img width="1522" height="936" alt="image" src="https://github.com/user-attachments/assets/3f0fc818-1958-4142-a84a-675963fa3c13" />

- Furthermore, we can also see failed attempts to remotely login to the Susan user account.
<img width="1918" height="1001" alt="image" src="https://github.com/user-attachments/assets/46df9b83-dd10-4736-9a97-fe9de4cc0037" />

- In the user account Susan, they attempted to SSH into the Ubuntu endpoint.
<img width="1522" height="927" alt="image" src="https://github.com/user-attachments/assets/386c4e59-1870-4860-91c3-e7b64939ddf8" />

- We can see a successfull SSH login.
  - I will now create a dashboard to help detect potentially malicious activity. 
  

# 8) Creating a dashboard
- I first created a dashboard to identify Windows activity.
<img width="1918" height="1000" alt="image" src="https://github.com/user-attachments/assets/e172850f-a6ce-47fa-8007-075de8548bd2" />

- By using a filter like the one above, I can use a dashboard that shows failed, and successful Windows authentication attempts, as well as Failed SSH logins.

<img width="1918" height="1002" alt="image" src="https://github.com/user-attachments/assets/d98f5d96-96c1-4de1-bbbf-025f886bb415" />

- I've created a Basic dashboard, and I will add some charts to help visualize the dashboard.
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/e58f0da3-125a-479d-b910-7eea7e45574b" />


#  9) Implementing File Integrity Monitoring
- To begin with the implementation of File Integrity Monitoring (FIM), I started with the Windows endpoint.
  - I created a directory called Company Data as an example directory for Wazuh to monitor.
<img width="1543" height="552" alt="image" src="https://github.com/user-attachments/assets/2ade19ce-7615-4c4e-9027-5e77ee31a8ca" />

- After creating the directory, I modified the **ossec.conf** file, and added the **Company Data** directory to realtime monitoring.
<img width="1377" height="373" alt="image" src="https://github.com/user-attachments/assets/b29edea7-3246-4438-b7a9-fa98889ed541" />

- In order to verify that FIM is working, I modified the Company Data directory by changing the contents of a file.
<img width="1918" height="1001" alt="image" src="https://github.com/user-attachments/assets/362db2ab-06bd-423f-81da-e75e9b51fe55" />

- We can see that FIM is working correctly on the Windows endpoint, and I began to configure FIM for the Ubuntu endpoint.
  - In the Ubuntu endpoint, I created a directory called **company-data**, and a file called **data.txt**
 <img width="1477" height="131" alt="image" src="https://github.com/user-attachments/assets/92871626-5665-4102-95f3-cec1b073e2da" />
 
- I modified the **ossec.conf** file to include the directory for FIM.
<img width="921" height="340" alt="image" src="https://github.com/user-attachments/assets/ec6c708f-7c97-4f96-a99c-5bdf585f93c3" />

- I tested to see if FIM was working.
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/7ef7488e-229c-4631-a177-6df6e30282c9" />

- After configuring FIM, I created a custom rule to check for the enabling of the Guest account on the Windows endpoint.
  - To help with the rule creation, I used ChatGPT to help with the creation of the rule.
<img width="1597" height="997" alt="image" src="https://github.com/user-attachments/assets/a769f6dd-706a-4b25-9f83-67f210139532" />

- I made sure ChatGPT followed the syntax of wazuh rules:
<img width="1267" height="447" alt="image" src="https://github.com/user-attachments/assets/d87c97b1-4171-4f25-8325-d498edea0e5f" />

- I added the newly created rule to the **custom_rules.xml** file.
<img width="1904" height="857" alt="image" src="https://github.com/user-attachments/assets/0a03a858-ca33-4d63-89bb-491c74ac6010" />

- We can see that the alert successfully fired off.
<img width="1917" height="927" alt="image" src="https://github.com/user-attachments/assets/8bdbe35b-f4c3-4c2f-8073-f3928fc2d388" />
<img width="1917" height="997" alt="image" src="https://github.com/user-attachments/assets/727d31a2-92b5-4534-9bdc-3aa8759f3176" />

