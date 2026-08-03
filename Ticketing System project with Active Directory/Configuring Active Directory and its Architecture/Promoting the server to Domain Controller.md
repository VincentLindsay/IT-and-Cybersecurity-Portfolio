# Overview
- This section features the promotion of a Windows server 2022 into a domain controller, and create a domain called **helpdesk.local**

# Promoting the server
- The first step in creating a domain is the installation of Active Directory Domain Services onto the Windows server
- I began with the addition of roles and features, and choose the role-based installation.
<img width="787" height="565" alt="image" src="https://github.com/user-attachments/assets/e71ccef1-3df5-4f69-ab0a-cf75b9219af0" />

- I installed the features of Active Directory Domain Services, and DNS server to make the DC the DNS server for the domain.
<img width="790" height="561" alt="image" src="https://github.com/user-attachments/assets/4430b04b-7b75-4419-96bf-5914da108e9d" />

- The installation of the features was complete, and now the next step is to create the forest.



- I added the new forest.
<img width="760" height="557" alt="image" src="https://github.com/user-attachments/assets/8a7da4d6-89fe-4970-926a-1041a6b7d2e7" />


- After the successful check of prequisites, the forest was created, and the Windows server was promoted to Domain Controller.
<img width="761" height="561" alt="image" src="https://github.com/user-attachments/assets/02be3767-b5cd-42c7-89a7-356a7a3de8d2" />

- I verified that the domain was created.
<img width="991" height="502" alt="image" src="https://github.com/user-attachments/assets/c498b670-9b2d-4381-bd5c-05abb901c90e" />


