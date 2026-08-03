# Overview
- This section will involve the installation of Splunk universal forwarder on all virtual machines used in this lab, except the Splunk server and the domain controller.

# Table of contents
- [Windows 10 UF installation](#Installing-Splunk-universal-forwarder-Windows-10-Endpoint)
- [Domain Controller UF installation](#Installing-Splunk-universal-forwarder-Domain-Controller)
- [Suricata Server UF instllation](#Installing-Splunk-universal-forwarder-Suricata-Server)

# Installing Splunk universal forwarder (Windows 10 Endpoint)
- To begin, I started with the installation of Splunk Universal Forwarders (UF) on the Windows 10 Endpoint.
- To verify connectivity, I pinged the Splunk Server from the Windows endpoint.
<img width="936" height="257" alt="image" src="https://github.com/user-attachments/assets/cd83c6f0-e2a7-4236-bf68-f34b1a98bb8e" />

- To see a detailed account of how I installed the UF, check out my splunk [lab](https://github.com/VincentLindsay/Security-Analysis-Portfolio/blob/main/Splunk%20lab/Setting%20Up%20Forwarder.md)

- A major difference between the original Splunk lab is the IP address of the Splunk server.
<img width="503" height="395" alt="image" src="https://github.com/user-attachments/assets/75adbbd2-ca5d-4d70-8f26-ae58eea8dfb9" />

- The UF was installed without any issues.
<img width="561" height="451" alt="image" src="https://github.com/user-attachments/assets/216fd1b3-9cc8-48ce-b286-b54291ec3b25" />

- These are the following configuration settings for the Windows endpoint.
<img width="752" height="521" alt="image" src="https://github.com/user-attachments/assets/1e20d847-1057-4284-9f58-dc134c1862e6" />


# Installing Splunk universal forwarder (Domain Controller)
- To be able to install the UF on the Domain Controller (DC), I have to install a different browser than internet explorer.
<img width="1021" height="728" alt="image" src="https://github.com/user-attachments/assets/901b0fe2-cf1b-4e60-b984-df15bde6e631" />

- I disabled the security zones in order to be able to access any website, and in this case install the UF.
- As a result, I downloaded chrome in order to be to access splunk[.]com
- Now I can proceed with installing the universal forwarder.
<img width="1020" height="771" alt="image" src="https://github.com/user-attachments/assets/fc6b55a6-399f-4e31-b77c-1da72b34aec2" />

- To simplify the identification of the host while doing Splunk searches, I changed the name of the DC.
<img width="1011" height="340" alt="image" src="https://github.com/user-attachments/assets/d071832f-96da-4a20-8419-3aa2519a7937" />

<img width="753" height="522" alt="image" src="https://github.com/user-attachments/assets/ea1381a3-c8d4-4b03-915e-c58f97606477" />

- Once the UF was installed, I added these configurations
- In Splunk, I can now see the DC, with the proper configurations I made.
<img width="1777" height="835" alt="image" src="https://github.com/user-attachments/assets/8c4ffa43-b591-42df-9801-6d324249fe0a" />

- I also installed sysmon to the DC.
<img width="1798" height="720" alt="image" src="https://github.com/user-attachments/assets/777df848-205c-485a-9a78-88f591ec6a55" />


# Installing Splunk universal forwarder (Suricata Server)
- To install the UF on the Suricata server, I utilized wget to obtain the UF installer.
<img width="1916" height="725" alt="image" src="https://github.com/user-attachments/assets/6d6723c7-c865-4305-863b-51554a78990f" />

- Next, I began to install the Splunk forwarder by installing the packages.
<img width="1170" height="150" alt="image" src="https://github.com/user-attachments/assets/53bc0bf2-2105-4728-ae98-bda66f264f6e" />

- I had the UF point towards the Splunk server.
- I also added the configurations necessary to forward the  Suricata logs.
<img width="882" height="486" alt="image" src="https://github.com/user-attachments/assets/adf124fd-6dab-4c4f-8015-491eb9163c41" />



- After restarting the service, the universal forwarder restarted without any issue.
- I verified the ingestion of the logs
<img width="1800" height="917" alt="image" src="https://github.com/user-attachments/assets/7112f85e-4906-4929-b897-4d57cfa4b49c" />



