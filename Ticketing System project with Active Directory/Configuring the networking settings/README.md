# Overview
- This section will involve the creation of a custome network using VMware's virtual network editor.
  - I will also assign static IP addresses to each of the virtual machines, and point them to the Domain Controller's IP address for DNS: 192.168.10.10
 
# Creating the VNET
- Using VMware's Virtual Network Editor, I can create a custom NIC, and subnet.
  - For this lab I will be using a 192.168.10.0/24 Subnet
  - I also configured DHCP settings
<img width="695" height="668" alt="image" src="https://github.com/user-attachments/assets/fdedc25e-dd7f-4769-946d-4b0c4b309b11" />


- Now that the VNET is created, I can now begin with the static assignment of IP addresses.

# Assigning IP addresses
- To begin, I will assign the machines with the following IP addresses:
  - 192.168.10.10 for the Domain Controller
  - 192.168.10.20 for the osTicket server
  - 192.168.10.30 for the Windows client
 
- I added the custom NIC to the Domain Controller
<img width="891" height="922" alt="image" src="https://github.com/user-attachments/assets/7b04beba-9cd9-4f20-b14a-41fa56d3358f" />

- To change the IP address on the server, I modified the adapter settings on the machine
<img width="1028" height="775" alt="image" src="https://github.com/user-attachments/assets/5bc1957f-b04f-4b58-b065-836ab83b0922" />

- Now the DC has a static IP address.
  - Using **ipconfig**, I verified the changes were made.

<img width="958" height="278" alt="image" src="https://github.com/user-attachments/assets/66bd88fa-6583-4b5e-9944-aab33669f2b5" />




- I changed the IP address of the Windows 11 client.
<img width="817" height="587" alt="image" src="https://github.com/user-attachments/assets/dc72ffe0-b6f2-4d2c-94d7-d8d400411199" />

- I verified using **ipconfig**
<img width="1028" height="332" alt="image" src="https://github.com/user-attachments/assets/213323d6-12e1-4b23-8304-99b055b57f0f" />

- Next, I began to change the ip address of the osTicket server.
- To change the IP address of the osTicket server, I needed to change the **yaml** file the the **/etc/netplan** directory.

<img width="1377" height="103" alt="image" src="https://github.com/user-attachments/assets/b6a02cf5-6f3d-42a1-99f5-ba09ff1249bf" />

- These are the configurations I chose to assign the server the IP address of **192.168.10.20**

<img width="936" height="358" alt="image" src="https://github.com/user-attachments/assets/0f386fa8-9a19-4598-a4c4-ad052b26b694" />

- The settings were successfully applied.


- Now I made sure all machines can communicate with each other.
- From the **DC**, I pinged the osTicket server.
<img width="1017" height="698" alt="image" src="https://github.com/user-attachments/assets/353b54ed-7c89-4427-8655-b2428e640e27" />

- To allow the Winndows machines to communicate with each other using ICMP pings, I enabled a firewall rule for inbound traffic
<img width="1005" height="717" alt="image" src="https://github.com/user-attachments/assets/2f24f909-3a80-49c2-adcb-e63724379546" />

- I also enabled the outbound rules to allow ICMP pings.
<img width="1010" height="526" alt="image" src="https://github.com/user-attachments/assets/f4e09b84-31fb-4a8a-a325-127cf3c8d1e1" />


- After this, I pinged the Windows machine from the DC
<img width="1037" height="153" alt="image" src="https://github.com/user-attachments/assets/f08b967c-55d0-4388-bf8c-186e7c3d0af5" />

- Now from the **Windows client**, I pinged both the DC, and the osTicket server.
<img width="988" height="622" alt="image" src="https://github.com/user-attachments/assets/114a6f9b-4285-43c7-b803-05f01bb721cf" />

- From the **osTicket** server, I pinged both the DC and the Windows client.
<img width="1192" height="562" alt="image" src="https://github.com/user-attachments/assets/44e78379-7243-4999-b4f6-6788029674f5" />

- Now the network settings are configured for this lab.






