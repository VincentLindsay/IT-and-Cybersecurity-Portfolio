# Overview
This section involves the development of the virtual machines used in this lab, the machines used will be an Ubuntu server (ver. 24.04.4), and a Windows 10 pro VM.

# Booting up Windows machine
* To build the Windows 10 vm, I acquired a Windows 10 ISO file
* By visiting the download Windows 10 page, I downloaded the media creation tool
* link: https://www.microsoft.com/en-us/software-download/windows10
* Once I downloaded the media creation tool, I selected the option to create an installation media
<img width="796" height="697" alt="image" src="https://github.com/user-attachments/assets/f0053d72-6d1e-480b-bc5e-e268d0235a98" />

* Since I may use the ISO file for other virtual machines, I unselected the option to use the recommended options for my PC

<img width="793" height="707" alt="image" src="https://github.com/user-attachments/assets/37c9c683-dd08-489a-ac95-fe09fd44f7b8" />

* I used the option to create an ISO file
<img width="797" height="703" alt="image" src="https://github.com/user-attachments/assets/e4b795e4-1ff6-4b48-a7ff-0b3679ffae0c" />

* Once downloaded, I began to create the virtual machine in VMware
<img width="392" height="503" alt="image" src="https://github.com/user-attachments/assets/a7d518a2-c5b7-41b1-b08a-17b0ab27f762" />

* Once booted, I selected the option of I don't have a product key
<img width="636" height="492" alt="image" src="https://github.com/user-attachments/assets/499ca693-3506-4c0d-9908-7de160731935" />

* I also selected the version of Windows 10 Pro
<img width="626" height="475" alt="image" src="https://github.com/user-attachments/assets/469388b8-4d9d-4cbd-9787-a340b562137c" />

* I also chose the custom Windows installation option
* I followed all of the options, and created a generic user account
  
<img width="463" height="426" alt="image" src="https://github.com/user-attachments/assets/60c89f46-1e50-418b-b020-07f6f7538dde" />

* Without any issues, I was able to install Windows, and I also installed VMware tools.
* I also created a snapshot of the VM

# Creating Ubuntu server
* For the Ubuntu server, I searched google for ubuntu server, and found the Get Ubuntu page
* link: https://ubuntu.com/download/server
* Currently, the latest version of Ubuntu server is 26.04, however I chose version 24.04.4 in the previous downloads page
<img width="1747" height="565" alt="image" src="https://github.com/user-attachments/assets/23254886-1338-4055-b4cc-39da326a6068" />

* After some time, the ISO downloaded to my PC
* Once downloaded, I began to configure the settings for the vm
 
<img width="513" height="475" alt="image" src="https://github.com/user-attachments/assets/07b24f77-63d6-4bc7-90cc-3d0aff90f331" />

* These are the settings I used based off my current specs of my host machine.
* Once booted, I followed the installation pages in the VM
* I did install OpenSSH to give myself the ability to SSH into the server via my host machine if needed.
<img width="1266" height="796" alt="image" src="https://github.com/user-attachments/assets/2ef41d05-e4f6-4bfc-a1b1-71a189d455e3" />

* Once the server was installed, I SSH'd into the server via Powershell
<img width="1127" height="625" alt="image" src="https://github.com/user-attachments/assets/1805372f-3e03-4662-a404-ac0a3346cbed" />

* I updated and upgraded the packages
* After the updates finished, I created a snapshot of the fresh ubuntu installation.
* Now that the machines are installed and configured, I can now proceed with installing splunk onto the server.


