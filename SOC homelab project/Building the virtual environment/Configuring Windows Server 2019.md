# Section summary  
I've downloaded and installed Windows Server 2019 to serve as the Domain Controller (DC) for the Active Directory Environment.

# Steps taken
- To retrieve the ISO file to run the server on VMware, I searched on google for "download windows server 2019", and reached Microsoft's evaluation center.
- Direct link: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019
- Since my language is United States English, I selected the 64-bit download that pertains to the langauage of my choice.
<img width="1881" height="567" alt="image" src="https://github.com/user-attachments/assets/88b7f3bc-3421-4117-89e6-0acb91cdb5b8" />

- Once you click the download link, the ISO will begin to download.
- Once the ISO downloaded, I started the process of creating the virtual machine.
- Since I am using VMware, I chose the manual option of installing the vm.
- In the following screenshot, I've included the specs for the VM based off of my hardware.
- I also disabled the side channel mitigations for additional performance.
<img width="1918" height="1041" alt="image" src="https://github.com/user-attachments/assets/c9555461-a416-4f19-96c2-e826b3f5aa8b" />

- In the installation, I chose the server graphical option.
<img width="636" height="482" alt="image" src="https://github.com/user-attachments/assets/b48fc928-3bea-4461-a479-31210a3d96a2" />

- Now I have successfully installed the server.
- I will promote this server to a domain controller later on.
<img width="1018" height="772" alt="image" src="https://github.com/user-attachments/assets/7a47be2f-792f-41a7-925e-078f01aef47e" />


