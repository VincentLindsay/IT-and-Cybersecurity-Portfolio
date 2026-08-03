# Overview
This section focuses on the creation of a virtual network for the homelab

# Steps taken
* Since this lab uses VMware Workstation Pro as the Hypervisor, I will use the virtual network editor built-in to VMware
<img width="692" height="657" alt="image" src="https://github.com/user-attachments/assets/9b7a9185-f35a-4413-ac6f-1ac1c1dada62" />

* Even though I may assign IP addresses statically, I still had DHCP enabled incase I wanted to add additional machines to the VNET.
* This lab will feature a 172.16.50.0/24 Subnet.
<img width="473" height="366" alt="image" src="https://github.com/user-attachments/assets/e11f08a5-4241-4cb3-84e2-d2a709b55853" />

* Additionally, I also utilized another virtual NIC to have NAT capability, and internet access
<img width="680" height="21" alt="image" src="https://github.com/user-attachments/assets/87c85c78-754d-4cc2-bb90-7e5ad853619b" />

