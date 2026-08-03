# Overview
This section involves the installation and configuration of a Windows 10 endpoint to serve as the victim machine in a later simulated attack.

# Steps taken
- To retrieve the ISO for Windows 10, I searched the web for "download windows 10".
- Direct link: https://www.microsoft.com/en-us/software-download/windows10
- I used to media creation tool to create the ISO file
<img width="790" height="703" alt="image" src="https://github.com/user-attachments/assets/3d7efb3b-7d35-4eb4-9958-8597a70c6170" />

- When I reached the choice of what to have the media tool do, I selected the option of creating an installation media
- Then have the tool create the ISO file
  


- After sometime, I created the virtual machine, and disabled side channel mitigations for additional performance.
- I will eventually add Splunk Universal Forwarder, and Sysmon to this vm.
- I will also add this machine to the domain I created.
<img width="642" height="486" alt="image" src="https://github.com/user-attachments/assets/a0ef5eff-2dd0-4e93-a0a2-3d049a66417a" />

- Since I do not have a product key, I chose the option of "I don't have a product key."
- I selected Windows 10 Pro as the edition of Windows for this homelab.
- After sometime, the vm reached the set up phase of Windows.
<img width="1035" height="777" alt="image" src="https://github.com/user-attachments/assets/94c4fee6-bced-410e-83e7-9adc29a8bb3a" />

- I chose the "Set Up for Work or School" option because I can create a local account, and Domain join later.

- For the name of the user account, I named it my name: Vincent.
- Once logged in, I began to optimise the performance of the vm, and I disabled Windows Updates via group policy edit.
<img width="685" height="632" alt="image" src="https://github.com/user-attachments/assets/4feb8234-b53b-4613-93de-e6a7407eb548" />

- I also installed VMware tools to improve the resolution, and performanace of the vm.
- Now the Windows machine is in a good state to configure Sysmon, and Splunk universal forwarder.



