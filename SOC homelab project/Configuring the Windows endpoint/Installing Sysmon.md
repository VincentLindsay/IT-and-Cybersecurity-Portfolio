# Overview
- This section features the Installation and configuration of Sysmon onto the Windows 10 endpoint.

# Installing Sysmon
- To install sysmon, I navigated to the sysinternals page for sysmon.
- Direct link: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
- For the configuration file, I will be using Olaf Hartong's sysmon-config.
- Direct link: https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml
- To download the configuration file, click view raw.
- Next, I saved the **.xml** file to the Windows vm.
- To install sysmon, I will use powershell to achive this.

<img width="825" height="527" alt="image" src="https://github.com/user-attachments/assets/c0fedcbf-fa1f-44c6-9141-eb073ab4f474" />

- In powershell I navigated to the directory will sysmon was downloaded.

<img width="825" height="276" alt="image" src="https://github.com/user-attachments/assets/b12f6718-4a2a-4ab3-8a1b-91ba5609cb87" />

- Sysmon was installed.
- I verified that sysmon was installed and automatically running using services.

<img width="880" height="472" alt="image" src="https://github.com/user-attachments/assets/0184cf33-8b03-4e4d-a7db-7a9e1faa9e88" />
