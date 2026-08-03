# Overview
This section revolves around the deployment of an Ubuntu server that is used for Splunk.

# Retrieving the ISO
- I obtained the Ubuntu servers from Ubuntu's download page.
- Direct link: https://ubuntu.com/download/server
- For this lab, I used Ubuntu server version 24.04.4.
- To obtain a previous version, navigate to the alternative downloads page on the server downloads.

<img width="975" height="332" alt="Image" src="https://github.com/user-attachments/assets/b02c8520-bb20-4444-94b6-c6ff321b2b00" />


- Once downloaded, I proceeded to install, and configure both servers.

# Setting up Splunk Server
- Once I configured the VM to the settings I wanted, I began to configure it in VMware.
  <img width="1903" height="535" alt="image" src="https://github.com/user-attachments/assets/ba82be15-468c-4ec1-8660-fbf425a7c02d" />

- I also installed the OpenSSH server so I can use my host terminal to SSH into the server for easier configuration.
- Once logged in, I used the **ip -a** command to obtain the IP address

<img width="1336" height="417" alt="image" src="https://github.com/user-attachments/assets/fcfe7348-8284-4b7e-9907-a524b2a29fd9" />

- I also updated the packages, and created a snapshot of the fresh install prior to installing Splunk.
<img width="1071" height="212" alt="image" src="https://github.com/user-attachments/assets/22eaf9e8-3040-4e98-b244-97dafaa1e1d9" />



