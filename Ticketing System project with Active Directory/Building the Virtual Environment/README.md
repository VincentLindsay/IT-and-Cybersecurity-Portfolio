# Overview
- This section will focus on the deployment of three VMs:
  - Windows server 2022.
  - Windows 11 Client.
  - Ubuntu Server 24.04.4 for osTicket.
 
# Deploying Servers
- I will first begin with the deployment of the Windows server 2022, which will become the Domain Controller.
- I obtained a 64-bit ISO from Microsoft's Evalation center: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
- Once Downloaded, I began to install it using VMware.

<img width="1918" height="1113" alt="image" src="https://github.com/user-attachments/assets/2004e934-5863-4d5c-abe9-67ac65b6eafc" />

- I chose the Windows server 2022 desktop experience with the GUI.
<img width="1031" height="782" alt="image" src="https://github.com/user-attachments/assets/9e97416d-f24a-42b6-8779-6f79f2562145" />

- I chose the custom option to install the server's files.
- I created the default Administrator account, and was able to boot up the server.
<img width="1018" height="768" alt="image" src="https://github.com/user-attachments/assets/187f3ea6-e604-44f9-b15d-665a29faa084" />

- I also created a snapshot to reflect the fresh installation.

- To install the Ubuntu server, I retrieved an ISO file from Ubuntu's download page: https://ubuntu.com/download/server
- Since I will be using version 24.04.4, I navigated to the alternative downloads section.
 <img width="1700" height="608" alt="image" src="https://github.com/user-attachments/assets/ba8317b3-2ec3-4072-8635-c231dc5a38ee" />

- I began to download the ISO, and then deploy the server.
<img width="1912" height="1030" alt="image" src="https://github.com/user-attachments/assets/e40af912-fcc4-437f-b64b-08a214380b84" />

- In the configurations, I installed OpenSSH server to make configurations easier by logging in remotely via my host machine. 
<img width="1916" height="1030" alt="image" src="https://github.com/user-attachments/assets/7516cb10-6dd8-46f4-a960-3261377f52ae" />

- Once booted, I ran updates to the server.
<img width="1366" height="1091" alt="image" src="https://github.com/user-attachments/assets/09fc3350-55ff-47af-bb0d-0662b766ed7f" />

- Once the updates were completed, I created a snapshot of the fresh installation of the server.
<img width="1918" height="1032" alt="image" src="https://github.com/user-attachments/assets/92995ae3-8547-4a74-9df1-601c393be534" />


# Deploying the Windows client
- To obtain an ISO for Windows 11, I retrieved an ISO from the download Windows 11 page: https://www.microsoft.com/en-us/software-download/windows11
<img width="1912" height="1017" alt="image" src="https://github.com/user-attachments/assets/6c899226-4fcc-4def-9d1e-24bd9c08e244" />

- Once downloaded, I began to deploy the client.
- Since Windows 11 requires TPM, I configured the files to support a virtual TPM with a password.
<img width="497" height="540" alt="image" src="https://github.com/user-attachments/assets/9176775c-6083-4bf4-a8b5-b07a1c6ae6b6" />

- I selected "I don't have a product key."
<img width="717" height="580" alt="image" src="https://github.com/user-attachments/assets/f13c5494-08d8-4275-a128-9409f36dd060" />


- I chose to install Windows 11.
<img width="1028" height="782" alt="image" src="https://github.com/user-attachments/assets/0f5e8b16-32ab-40e5-87b3-f5599db6e9a4" />

- I named the VM to be **CLIENT01**
<img width="1028" height="776" alt="image" src="https://github.com/user-attachments/assets/74cdb6c3-c1b4-446c-a76f-eb565bf64718" />

- I Chose to set up for Work or School.
<img width="938" height="685" alt="image" src="https://github.com/user-attachments/assets/351384c1-730d-41a2-979e-d36b3bc7c849" />

- I selected domain join instead to be able to create a local windows account.
<img width="942" height="683" alt="image" src="https://github.com/user-attachments/assets/b49df762-6db2-49e4-98ed-03997caf05c0" />

- I created a simple account for the intial configurations.
- After sometime, the VM was fully installed, and ready for further configurations.
<img width="1025" height="772" alt="image" src="https://github.com/user-attachments/assets/57f0fb51-e748-4953-a606-ed1fd006e178" />



